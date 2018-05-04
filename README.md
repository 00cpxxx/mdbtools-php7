# mdbtools-php7

If you, as me, still requires to open and export ancient MDB databases in 2017 fear no more, I have (poorly) ported the code to PHP7 development environment and it worked in tests with all databases I required so far. The original package can be found at: 
https://pecl.php.net/package/mdbtools

My attempts to contact the original author (Hartmut Holzgraefe) got no reply, so I'm uploading here to avoid losing the code. All kudos to him, all I did was add a bunch of #ifdef.

To compile just use phpize, ./configure and make as any other pecl extension. You will need the php7 development files and also the mdbtools development files. After compiling "make install" and ensure you turn on the extension in your php.ini file. From there it is as simple as it can be on structured code:

<pre>
$link = mdb_open('database.mdb');
$tables = mdb_tables($link);
foreach($tables as $table_name)
{
  $handle = mdb_table_open($link, $table_name);
  echo 'TABLE = ', $table_name, PHP_EOL;
  echo 'ROWS = ', mdb_num_rows($handle), PHP_EOL;

  while(($record = mdb_fetch_assoc($handle)))
    var_dump($record);

  mdb_table_close($handle);
}
mdb_close($link);
</pre>

Sample code carelessly written by memory and without error check ;-)
