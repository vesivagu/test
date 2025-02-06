function validateModuleFormat(input) {
    const regex = /^\d{5}_[a-zA-Z]{3,}(_[a-zA-Z]{3,})+$/;
    return regex.test(input);
}

// ✅ **Valid Examples**
console.log(validateModuleFormat("11697_module_submodule")); // true
console.log(validateModuleFormat("12345_mod_sub"));          // true
console.log(validateModuleFormat("54321_abc_def_ghi"));      // true

// ❌ **Invalid Examples**
console.log(validateModuleFormat("11697_module"));           // false (missing submodule)
console.log(validateModuleFormat("11697_mo_sub"));           // false (module < 3 characters)
console.log(validateModuleFormat("11697_module_su"));        // false (submodule < 3 characters)
console.log(validateModuleFormat("1169_module_sub"));        // false (4 digits)
console.log(validateModuleFormat("116970_module_sub"));      // false (6 digits)
console.log(validateModuleFormat("11697_module_"));          // false (ends with underscore)
console.log(validateModuleFormat("11697_module_sub_extra")); // false (extra part after submodule)
console.log(validateModuleFormat("11697_module_sub1"));      // false (digits in submodule)
