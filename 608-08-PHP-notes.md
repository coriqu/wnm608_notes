# PHP notes for m08

- **Read data**

  ```php
  $url = 'data/user.json'; // path to your JSON file
  $getdata = file_get_contents($url); 
  									// put the contents of the file into a variable
  $data = json_decode($getdata,true);// change JSON String to PHP Array
  ```

- **Write data**
  
  ```php
  $string = json_encode($data); //change PHP Array to JSON String
  file_put_contents('data/user.json',$string);//write
  ```
  
- **Add data**
  
  [array_push()](https://www.php.net/manual/en/function.array-push.php):  Push one or more elements onto the end of array
  
  ```php
  array_push($data, array('user' => $name, 'email' => $email ));
  ```
  
- **Update data**

  To check and updata an element from JSON file, you need to get the current data `$index` and find it in the data as `$data[$index]`.

  ```php
  foreach ($data as $i=>$currentdata) {
  			if($index==$i) {
  				$data[$i]['user'] = $name;
  				$data[$i]['email'] = $email;
  			}
  }
  ```

- **Delete date**

  [unset()](https://www.php.net/manual/en/function.unset.php) Unset a given variable

  ```php
  unset($data[$index]); //delete
  $users2 = array_values($data); //re-index data
  ```





### Other Information

- **Mac configuration PHP development environment**

  https://mallinson.ca/posts/5/the-perfect-web-development-environment-for-your-new-mac

- **Read & write data in local computer**

  If you have Mac OS X, go to the file root or the folder of your website. Then right-hand click on it, go to get information, go to the very bottom (*Sharing & Permissions*), open that, change all read-only to read and write. Make sure to open padlock, go to setting icon, and choose *Apply* to the enclosed items...

  

  

  

  ### **JUST SOME COPY FROM THE INTERNET BELOW**

  If you want to re-index starting to zero, simply do the following:

  ```php
  $data = array_values($data);
  ```

  If you need it to start at one, then use the following:

  ```php
  $data_start_at_1 = array_combine(range(1, count($arr)), array_values($arr));
  ```

  Implode 将一个一维数组的值转化为字符串

  ```php
  $array = array('lastname', 'email', 'phone');
  $comma_separated = implode(",", $array);
  
  echo $comma_separated; // lastname,email,phone
  ```

  explode— 使用一个字符串分割另一个字符串

  ```php
  $pizza  = "piece1 piece2 piece3 piece4 piece5 piece6";
  $pieces = explode(" ", $pizza);
  echo $pieces[0]; // piece1
  echo $pieces[1]; // piece2
  ```

```php
// 追加写入用户名下文件
$code="001";//动态数据
        $json_string = file_get_contents("text.json");// 读取数据到PHP变量
        $data = json_decode($json_string,true);// 把JSON字符串转成PHP数组
        $data[$code]=array("a"=>"as","b"=>"bs","c"=>"cs");
        $json_strings = json_encode($data);
        file_put_contents("text.json",$json_strings);//写入
//修改

  $json_string = file_get_contents("text.json");// 读取数据到PHP变量
        $data = json_decode($json_string,true);// 把JSON字符串转成PHP数组
        $data["001"]["a"]="aas";
        $json_strings = json_encode($data);
        file_put_contents("text.json",$json_strings);//写入
```

to check and remove an element from JSON file.

```php
$i=0;
foreach($data as $element) {
   //check the property of every element
   if($url == $element->indirizzo_paginaauto){
      unset($data[$i]);
      echo ("elemento cancellato");
   }
   $i++;
}
```



加了post点取消按钮,页面刷新，从`http://localhost/coriq/views/admin/user.php?add=`变成

`http://localhost/coriq/views/admin/user.php`

```php+HTML
<form action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]);?>" method="post">
  <tr>
    <td>User</td>
    <td><input id="user" type="text" name="user"></td>
  </tr>
  <tr>
    <td>Email</td>
    <td><input id="email" type="text" name="email"></td>
  </tr>
  <tr>
    <td class="textright"><button class="btn cancel">Cancel</button></td> 
    <td><button class="btn submit" id="ajaxButton">Submit</button></td>
  </tr>
</form>
```

把post取消,点取消按键，变成`http://localhost/coriq/views/admin/user.php?user=&email=`

```php+HTML
<form action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]);?>">
```

把cancel按键改一下,`http://localhost/coriq/views/admin/user.php?add=`不变

```html
<button class="btn cancel" onclick="return false;">Cancel</button>
```

把submit按钮改一下加上`type="button"`,不提交了

```html
<button type="button" class="btn submit" id="ajaxButton" name="submit">Submit</button>
```



