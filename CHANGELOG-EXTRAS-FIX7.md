# Mekanism Extras 1.4.2-fix7

Fixes factory batch processing consuming energy for one recipe while producing multiple recipe operations. Each actually processed operation now uses the normal Mekanism recipe energy cost, including speed and energy upgrade scaling. Multiple active process lanes add their actual usage. Energy-limited processing performs only affordable work, and idle factories consume no recipe energy. Creative upgrade behavior is preserved.

New server config `versionLockedBalance.batchOperationsCost=true` in Extras general config enables this behavior by default. Explicit false selects the legacy flat per-process cost. Restart after changing so existing recipe caches capture the policy.

Applied to 19 factory cache construction paths, covering native Extras, MoreMachine and advanced chemical factories. No non-factory batch-operation paths were found in Extras source. Based on the existing fix6 jar; matrix pull and all other unrelated fixes, resources, mixins and generated computer handlers are retained byte-for-byte. Final overlay changes only the intended20 top-level production classes and two version metadata entries. No new dependencies, stubs or test mod are shipped.

Optional EvolvedMekanism AlloyingFactory had an uncached external compile dependency absent from installed ATM11. Its existing class received the identical four-instruction config lookup and setOperationsCost call after setEnergyRequirements; all original code/linkage remains intact. It was bytecode-inspected but not functionally instantiated without its optional dependency.

Validation: isolated NeoForge26.1.2.109 dedicated server, Core2.9, current MoreMachineport8 and Generators1.4. Real enrichment cached recipes run across absolute/supreme/cosmic/infinite tiers and STACK0..8. Tests verify actual outputs and energy deltas, standard Mekanism upgrade and throughput formulas, insufficient energy, affordable work limits, idle behavior, two simultaneous process lanes, explicit legacy config and creative output/energy preservation. 257 assertions pass. The original fix6 reproduction produced four outputs while charging one operation (parent baseline-energy.log).
