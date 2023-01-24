# ServiceCollectionAssemblyScanning
DIコンテナに登録するクラス群を、参照先のアセンブリからスキャンして自動登録します。

# Usage
```C#
// 自動DI登録対象のアセンブリを取得
var assemblies = System.Reflection.Assembly.GetExecutingAssembly().CollectReferencedAssemblies(
        new[]{ "MyRepogitory", "MyLogic" }
    );

// MyRepogitoryアセンブリ中の、IRepogitoryを実装している全ての型をScopedで登録
services.AddAssemblyTypes<IRepogitory>(assemblies.GetByName("MyRepogitory"), ServiceLifetime.Scoped);
// MyLogicアセンブリ中の、末尾にLogicが付く全ての型をScopedで登録
services.AddAssemblyTypes(assemblies.GetByName("MyLogic"), ServiceLifetime.Scoped, "Logic");
// 対象の全てのアセンブリ中の、先頭がFakeで始まる全ての型をScopedで登録
services.AddAssemblyTypes(assemblies, ServiceLifetime.Scoped, t => t.Name.StartsWith("Fake"));
```
