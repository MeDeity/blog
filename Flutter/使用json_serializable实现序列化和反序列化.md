#### 使用json_serializable实现序列化和反序列化

一、添加必要的依赖
```
dependencies:
  # Your other regular dependencies here
  json_annotation: ^2.0.0

dev_dependencies:
  # Your other dev_dependencies here
  build_runner: ^1.0.0
  json_serializable: ^2.0.0
```
>你可能需要运行flutter packages get命令手动获取依赖包

示例Model
```
import 'package:json_annotation/json_annotation.dart';
//运行命令后会自动生成,(className.g.dart),但需要手动引入
part 'data.g.dart';

@JsonSerializable()
class Data{
  final String by;
  final int descendants;
  final int id;
  final List<int> kids;
  final int score;
  final int time;
  final String title;
  final String type;
  @JsonKey(nullable: false)
  final String url;

  Data({this.by, this.descendants, this.id, this.kids, this.score, this.time,
    this.title, this.type, this.url});

  //需要手动书写
  factory Data.fromJson(Map<String, dynamic> json) => _$DataFromJson(json);
  
  //需要手动书写
  Map<String, dynamic> toJson() => _$DataToJson(this);
}
```

使用控制台执行以下代码
```cmd
flutter packages pub run build_runner build
```

>执行以上命令后，会自动生成[className].g.dart,在该文件中定义了序列化及反序列化的方法,总体上如果不依靠插件,这样进行序列化及反序列化还是挺麻烦的.


#### 使用FlutterJsonBeanFactory进行序列化及反序列化
1.在Idea上安装FlutterJsonBeanFactory插件,使用该插件可以简化序列化及反序列化的操作,详情可以查看该插件作者的博客信息[FlutterJsonBeanFactory插件json使用](https://www.jianshu.com/p/14cbcbaa74b7)