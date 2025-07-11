# How to Contribute to Meowdding

If you have any questions, feel free to ask us in our [Discord](https://meowdd.ing/discord).

## Prerequisites

Before starting out, you should have a basic understanding of Java/Kotlin (or programming in general).

- IDE: [Intellij IDEA (Ultimate/Ultimate Edition)](https://www.jetbrains.com/idea/download/) is the best Kotlin Editor out there.
   - Either use the Community Edition (scroll down a bit) or if you want to pay/are a student, you can also get the Ultimate Edition

- TODO: cloning and stuff maybe idk

## Dependencies

Since Meowdding is a collection of mods instead of a singular mod, we use multiple dependencies for different purposes:

> #### [SkyBlockAPI](https://github.com/SkyblockAPI/SkyblockAPI):
> Contains all SkyBlock related API's, like BazaarAPI, CurrencyAPI, SlayerAPI, ... basically anything one might need for SkyBlock development.

> ### [MeowddingLib](https://github.com/meowdding/meowdding-lib)
> Contains mostly rendering related stuff (Displays, Layouts) and other Util that wouldn't really fit into SkyBlockAPI.


When adding a feature for one of our mods, you might find that the API part isn't implemented yet (we have most, but not everything).
Feel free to write the API part in the feature mod to see if it works, before opening a PR into SkyBlockAPI (SbAPI) or MeowddingLib (MLib).
