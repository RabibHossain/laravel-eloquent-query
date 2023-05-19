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
  
