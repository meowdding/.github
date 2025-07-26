# How to Contribute to Meowdding

If you have questions, join our [Discord](https://meowdd.ing/discord).

## Prerequisites

Basic Java/Kotlin knowledge is required.

- **IDE**: Use [IntelliJ IDEA](https://www.jetbrains.com/idea/download/)
  - Community Edition (free) or Ultimate Edition (paid/student license)
- **JDK**: Install [JDK 21](https://jdk.java.net/archive/)

## Setting Up

1. Clone the repository
2. Open the project in IntelliJ
3. Set up JDK 21 in Project Settings

## Writing Code & Booting up the Game

To support multiple Minecraft versions at once, we use [Cloche](https://github.com/terrarium-earth/cloche), a lib for Minecraft Multiversion using Kotlin Multiplatform.
Code shared between the Minecraft versions is in src/common/main or src/main (depending on the project), version specific code in src/<version>.

If Code will be relatively different between two versions, you should use KMP. E.g.:

<details>
<summary>Using KMP</summary>  

[src/common/.../EntityPlatform.kt](https://github.com/SkyblockAPI/SkyblockAPI/blob/5d2b9b9a51852eb6a0b889e14ccf52f2b3013856/src/common/main/kotlin/tech/thatgravyboat/skyblockapi/platform/EntityPlatform.kt)
```kt
@Stub expect fun Entity.save(): CompoundTag
```

[src/1.21.5/.../EntityPlatform.kt](https://github.com/SkyblockAPI/SkyblockAPI/blob/5d2b9b9a51852eb6a0b889e14ccf52f2b3013856/src/1.21.5/main/kotlin/platform/EntityPlatform.kt)
```kt
actual fun Entity.save(): CompoundTag {
    val tag = CompoundTag()
    tag.putString("id", EntityType.getKey(this.type).toString())
    return this.saveWithoutId(tag)
}
```

[src/1.21.8/.../EntityPlatform.kt](https://github.com/SkyblockAPI/SkyblockAPI/blob/5d2b9b9a51852eb6a0b889e14ccf52f2b3013856/src/1.21.8/main/kotlin/platform/EntityPlatform.kt)
```kt
actual fun Entity.save(): CompoundTag {
    val collector = ProblemReporter.ScopedCollector(SkyBlockAPI)
    val valueOutput = TagValueOutput.createWithoutContext(collector)
    valueOutput.putString("id", EntityType.getKey(this.type).toString())
    this.saveWithoutId(valueOutput)
    collector.close()
    return valueOutput.buildResult()
}
```

</details>

IntelliJ might scream at you with `'actual fun Entity.save(): CompoundTag' has no corresponding expected declaration`. It's a little stupid, you can ignore this Error, your game still boots.

If Code will be minor (y=10 instead of y=12), you can use `tech.thatgravyboat.skyblockapi.utils.McVersionGroup.MC_<version>.isActive` instead.

## Dependencies

Meowdding mainly uses these custom libraries:

### [SkyBlockAPI](https://github.com/SkyBlockAPI/SkyblockAPI)
Handles SkyBlock features:
- API's like BazaarAPI, CurrencyAPI, SlayerAPI, etc.
- Other SkyBlock utilities

### [MeowddingLib](https://github.com/meowdding/meowdding-lib)
Provides:
- Rendering systems (Displays, Layouts)
- Common utilities

## Adding Features

If an API feature is missing:
1. Implement it temporarily in your feature mod
2. Test if it works
3. Open a PR to the appropriate library

