# MockableJarGenerator
**MockableJarGenerator** is a modified version of official [MockableJarGenerator][1] which can generate a "mockable" version `android.jar` **(with enables internal and hidden APIs)**. You can find those `android.jar` in this project: [anggrayudi/android-hidden-api][2]

## Background

Why we need this project? Because when you use a hidden-api's `android.jar`, the gradle task `mockableAndroidJar` will throws following error.

```
Error:Execution failed for task ':app:mockableAndroidJar'.
> java.lang.NullPointerException (no error message)

```

So your unit testing may fail if you're trying to mock or depends on any android platform class. This error was throws by [asm][3] operation when generator trying to writes a modified *.class file to the output JAR file.

This modified generator fixed the issus and you can manually place the generate `mockable-android-xx.jar` to following directory: `projectRootDir/build/generated/`.

## Usage

```java
MockableJarGenerator generator = new MockableJarGenerator(false);
File input = new File("android-xx.jar");
File output = new File("mockable-android-xx.jar");
try {
   generator.createMockableJar(input, output);
} catch (IOException e) {
   e.printStackTrace();
}
```

## Feedback

Any issues or PRs are welcome!

## License

    Copyright 2017 codezjx <code.zjx@gmail.com>

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

[1]: https://android.googlesource.com/platform/tools/base/+/android-7.1.1_r58/build-system/builder/src/main/java/com/android/builder/testing/MockableJarGenerator.java
[2]: https://github.com/anggrayudi/android-hidden-api/
[3]: http://asm.ow2.org/