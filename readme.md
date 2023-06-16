## Create | Update Data Using Eloquent Request

- [x] Create data using eloquent request
  ```sh
  public function insert(ModelRequest $request)
  {
    Model::create($request->all());
  }
  ```
  
- [x] Update Data using eloquent request
  ```sh
  public function update(ModelRequest $request, Model $modelInstance)
  {
    $modelInstance->fill($request->all())->save();
  }
  ```

## Update Existing Column

- [x] Setting email to unique
  ```sh
  public function up()
    {
        Schema::table('users', function (Blueprint $table) {
            $table->unique('email', 'users_email_uniq');
        });
    }
    
  public function down()
    {
        Schema::table('users', function (Blueprint $table) {
            $table->dropUnique('users_email_uniq');
        });
    }
  ```
  
- [x] Adding new Column to a table with a default value
  ```sh
  public function up()
    {
        Schema::table('users', function (Blueprint $table) {
            $table->string('phone')->after('password')->default(null);
        });
    }
    
  public function down()
    {
        Schema::table('users', function (Blueprint $table) {
            $table->dropColumn('phone');
        });
    }
  ```
  
- [x] Modify the column to make it nullable
  ```sh
  public function up()
    {
        Schema::table('users', function (Blueprint $table) {
            $table->time('phone')->nullable()->change();
        });
    }
    
  ```  
  
## Retrieve Single Model Instance

- [x] Retrieve a model by its primary key or id
  ```sh
  $instance = ModelName::find(1);
  ```
  
- [x] Retrieve the first model data matching the condition
  ```sh
  $instance = ModelName::where('active', 1)->first();
  ``` 
  Or, an alternative to above statement by using <b>firstWhere</b>. It do the same (Matching the condition).
  ```sh
  $instance = ModelName::firstWhere('active', 1);
  ```  
  
- [x] Throw an exception if a instance of model is not found
  ```sh
  $instance = ModelName::findOrFail(1);
  ```  
  Or,
  ```sh
  $instance = ModelName::where('age', '>', 30)->firstOrFail();
  ```  
  
## Full Text SEARCH over columns

- [x] Put below statements inside **public function up()** of migration
  ```sh
  # Laravel doesn't support full text search migration
  
  // Single Column
  DB::statement('ALTER TABLE TABLE_NAME ADD FULLTEXT search_index(columnName)'); 
  // Multiple Column
  DB::statement('ALTER TABLE TABLE_NAME ADD FULLTEXT search_index(column1, column2)'); 
  ```
- [x] Put below statements in **public function down()** of migration
  ```sh
  Schema::table('model_name', function($table) {
	    $table->dropIndex('search_index');
	});
  ```
- [x] Now write the eloquent statement in **controller** / **service class** / **actions class**.
  ```sh
  // Single Column
  ModelName::whereRaw('MATCH (columnName) AGAINST (?)' , array($request->search_text))->get();
  // Multiple Column
  ModelName::whereRaw('MATCH (column1, column2) AGAINST (?)' , array($request->search_text))->get();
  ```  
  
  
## JSON Where Clauses  
  
- [x] Find in Nested JSON Array with multiple Key <a href="https://github.com/RabibHossain/laravel-eloquent-query/blob/main/userlist.json">userlist.json</a>
  ```sh
  DB::table('my_table_name')
            ->whereJsonContains('column_name->data', ['first_name' => 'Michael', 'last_name' => Lawson])
            ->get();
  ```
  
- [x] Find in Nested JSON Array with single Key <a href="https://github.com/RabibHossain/laravel-eloquent-query/blob/main/userlist.json">userlist.json</a>
  ```sh
  DB::table('my_table_name')
            ->whereJsonContains('column_name->data', ['email' => 'michael.lawson@reqres.in'])
            ->get();
  ```
  
- [x] Find in JSON Key <a href="https://github.com/RabibHossain/laravel-eloquent-query/blob/main/singleuser.json">singleuser.json</a>
  ```sh
  DB::table('my_table_name')
            ->whereJsonContains('column_name->data->email',  'janet.weaver@reqres.in')
            ->get();
  ```
  
- [x] Find in JSON vis LIKE Search <a href="https://github.com/RabibHossain/laravel-eloquent-query/blob/main/singleuser.json">singleuser.json</a>
  ```sh
  ModelName::where('column_name->data->email', 'like', '%weaver@reqres%')
            ->get();
  ```
  
