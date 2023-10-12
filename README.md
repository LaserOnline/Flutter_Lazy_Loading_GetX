
## Flutter Lazy Loading With GetX

install package GetX
```bash
import 'package:get/get.dart';
```

## Code Example
main.dart
```bash
void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return GetMaterialApp(
      debugShowCheckedModeBanner: false,
      initialRoute: 'register',
      getPages: AppRoutes.routes,
    );
  }
}
```
router.dart
```bash
class AppRoutes {
  static final routes = [
    GetPage(
      name: '/register',
      page: () => RegisterView(),
      binding: RegisterBinding(),
    ),
  ];
}
```

binding.dart
```bash
class RegisterBinding implements Bindings {
  @override
  void dependencies() {
    Get.lazyPut<RegisterController>(() => RegisterController());
  }
}
```

## FAQ

#### คำสั้ง ? Get.lazyPut<RegisterController>(() => RegisterController());

คือคำสั่งที่บอกว่า RegisterController ควรถูกสร้างแบบ lazy loading, ซึ่งหมายความว่ามันจะไม่ถูกสร้างจนกว่าจะมีการเรียกใช้งานจริง ๆ เช่น ผ่าน Get.find<RegisterController>()

#### binding ใน GetPage คืออะไร ?

binding บ่งบอกว่าเมื่อหน้า RegisterView ถูกเรียกใช้, การเชื่อมต่อ RegisterBinding 
จะถูกสั่งให้ทำงาน. ภายใน RegisterBinding, และได้กำหนดว่า RegisterController ควรถูกสร้างขึ้นโดยใช้ lazy loading
