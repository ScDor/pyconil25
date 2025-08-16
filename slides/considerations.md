# Trade-offs
<v-clicks>
- **Performance**
- **Dependency cost** - size, speed, security, license, overlap
- **Stability** - Churn vs maintain
- **When Magic Backfires** - With great power
- **Understandability** - The bus factor
- **Portability** - OS, Python version
- **Extensibility** - Escape hatches
- **When `stdlib` wins** - Keep it simple & stupid (sometimes)
</v-clicks>

<!--
When coming to choose a lib
Dependency weight: deps bring install size, cold starts, license risks, CVEs.

Stability: API churn, long-term maintainability, and whether the team still understands it years later.

Performance: Hot loops example. Helpers can add overhead in critical paths. Outside hot loops, fine.  

When Magic Backfires: Silent default behaviors, testability (the more magic)

Portability: Mention version support, typing, different OS issues. 

Extensibility: Does the library let you drop back down to the stdlib when needed? Does it play nicely with other tools in the ecosystem? That flexibility is a big factor.  

When stdlib wins: If it’s 5–10 clear lines, skip the dependency. Zero deps is a feature.  
-->
