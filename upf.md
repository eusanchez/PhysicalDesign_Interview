# UPF (Unified Power Format)
## Concepts of UPF
1. Power domains : UPF allow designers to define different power domains, they can be clamped to 1 or 0. Depending on the value it helps to reduce power consumption during idle state. 

Structure:
```
create_power_domain name_power_domain -elements {name_wrapper}
```

Example:
```
create_power_domain pd_top -include_scope #top must always be included
create_power_domain pd_aon -elements {aon_wrapper}
```

2. Level Shifters: These are utilized to manage voltage differences between various power domains.

```
set_level_shifter LtoH_sig_to_powerdomain \
-domain pd_gated_aon_powerdomain \
-applies_to inputs \
-rule low_to_high \
-location self

set_level_shifter HtoL_sig_from_powerdomain \
-domain pd_gated_aon_powerdomain \
-applies_to outputs \
-rule high_to_low \
-location self
```

3. 