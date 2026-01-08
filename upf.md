# UPF (Unified Power Format)
## Concepts of UPF
1. **Power domains**: UPF allow designers to define different power domains, they can be changed to 1 or 0. Depending on the value it helps to reduce power consumption during idle state. 

Structure:
```
create_power_domain name_power_domain -elements {name_wrapper}
```

When declaring the top, we don't use the ```element``` we use the ```-include_scope```.

Example:
```
create_power_domain pd_top -include_scope #top must always be included
create_power_domain pd_aon -elements {aon_wrapper}
```

2. **Level Shifters**: These are utilized to manage voltage differences between various power domains.

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

3. **Isolation Cells**: Speciall logic cells inserted on signals crossing from a power-gated domain to an always-on-domain. Their job is to force signals to a known value, when the source domain is OFF.

If the power is OFF, signals might become UNKNOWN which is dangerous, these can be propagated and break simulation. *Isolation cells prevent X-propagation*

Also known as *clamp cell*.

Structure:
```
set_isolation isol_clamp#_sig_from_powerdomain \
-domain which_domain \
-isolation_power_net what_rails_power_the_clamp_cell \
-isolation_ground_net what_rails_power_the_clamp_cell \
-clamp_value value_to_clamp \
-elements {which_signals}

set_isolation_control isol_clamp1_sig_from_pgd \
-domain which_domain \
-isolation_signal which_signal_constrols_it \
-isolation_sense polarity \
-location parent
```

Example:

```
set_isolation isol_clamp1_sig_from_pgd \
-domain pd_gated \
-isolation_power_net VCCL \
-isolation_ground_net GND \
-clamp_value 1 \
-elements {pgd_wrapper/sig2}

set_isolation_control isol_clamp1_sig_from_pgd \
-domain pd_gated \
-isolation_signal aon_wrapper/pmu/isol_pgd_en \
-isolation_sense low \ #isolation enabled when isol_pgd_en==0
-location parent #cell is placed in the parent (always-on) domain
```

We need both ```set_isolation_control``` and ```set_isolation```. ```set_isolation``` defines what to isolate and how to clamp and ```set_isolation_control``` defines when it happens. 