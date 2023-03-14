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
  
  
  
