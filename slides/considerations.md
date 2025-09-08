# Considerations

<v-clicks>

- **Understandability** - The bus factor
- **When `stdlib` wins** - Keep it simple & stupid (sometimes)

- **Dependency cost** - Size, speed, security, license, overlap, breaking changes
- **When Magic Backfires** - With great power--
- **Extensibility** - Escape hatches
</v-clicks>

<!--
Sometimes, stdlib wins: If it’s 5–10 clear lines, skip the dependency. Zero deps is a feature.  
When coming to choose a lib
Dependency weight: deps bring install size, cold starts, license risks, CVEs.

Stability: API churn, long-term maintainability, and whether the team still understands it years later.

When Magic Backfires: Silent default behaviors, testability (the more magic)

Extensibility: Does the library let you drop back down to the stdlib when needed? Does it play nicely with other tools in the ecosystem? That flexibility is a big factor.  

-->
