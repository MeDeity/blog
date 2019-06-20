
一、添加不要的依赖
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
//运行命令后悔自动生成
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

  
  factory Data.fromJson(Map<String, dynamic> json) => _$DataFromJson(json);
  
  Map<String, dynamic> toJson() => _$DataToJson(this);
}
```

使用控制台执行以下代码
```cmd
flutter packages pub run build_runner build
```

>执行以上命令后，会自动生成[className].g.dart,在该文件中定义了序列化及反序列化的方法