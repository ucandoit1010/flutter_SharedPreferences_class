## Flutter with SharedPreferences
### 1. create a new dart file and copy below code 新增一個 Dart 檔案複製以下程式碼貼上
``` import 'package:shared_preferences/shared_preferences.dart';
//參考 https://docs.flutter.dev/cookbook/persistence/key-value
class DataOperator {
  static SharedPreferences? sp;
  static Future init() async {
    sp = await SharedPreferences.getInstance();
  }

  static Future saveData(String key , String val) async {
    // await sp?.setString(key, val);
    await sp?.setString(key, val);
  }

  static Future<String> readData(String key) async {
    if(sp == null){
      return 'Null';
    }
    return sp?.getString(key) ?? 'No Value';
  }
}
```

### 2. Open your main.dart 回到 main.dart 找到 main function

``` 
Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await DataOperator.init(); //Add this line. 加入這一行

  runApp(MyApp());
}
```

### 3. You can use DataOperator class everywhere 在任何 dart 裡面呼叫


``` 
import 'Models/DataOperator.dart';
....skip...
onTap: ()
{
   DataOperator.saveData('key', 'text');
}

```

### Note
You must restart your app in the AVD before debug.
Because the class is static file.
因為靜態類別 所以要 Debug 之前重開虛擬機裡面的 app
