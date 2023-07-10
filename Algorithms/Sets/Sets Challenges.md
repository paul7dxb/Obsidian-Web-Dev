# Double Occurances in Arrays

- Output dishes where ingredient occurs in atleast twice
- Output to be sorted by ingredient alphabetically

```JS
const { result } = require("lodash")

function solution(dishes) {
    ingredients = {}
    doubleMenusSet = new Set()
    
    for ( dishIndex = 0; dishIndex < dishes.length ; dishIndex ++){
        dishName = dishes[dishIndex][0]
        for (ingredientIndex = 1; ingredientIndex < dishes[dishIndex].length; ingredientIndex++){
            ingredient = dishes[dishIndex][ingredientIndex]
            
            // Check if already exists (is a multiple dish ingredient)
            if(ingredients[ingredient]){
                ingredients[ingredient].push(dishName) 
                doubleMenusSet.add(ingredient)
            } else{
                // First entry
                ingredients[ingredient] = [dishName]
            }
        }
        
        
    }

    // Change doubleMenusSet set to organised array
    doubleMenus = Array.from(doubleMenusSet).sort()
    console.log(doubleMenus)
    
    // console.log(doubleMenusSet)
    organsisedMenu = []
    doubleMenus.forEach( (ingredient) => {
        console.log(ingredient)
        // console.log(ingredients[ingredient].sort())
        menuOption = ingredients[ingredient].sort()
        menuOption.unshift(ingredient)
        organsisedMenu.push(menuOption)
        
    })
    
    return organsisedMenu
    
}

```

# Check if consistent mapping between two arrays

- For strings and patterns check
	- All equal patterns go to the same string
	- All equal strings go to the same pattern

```JS
function solution(strings, patterns) {
    var hash = {}, 
        reverse = {};
    return strings.every((s, i) => {
        var p = patterns[i];
        if (!hash[p]) hash[p] = s;
        if (!reverse[s]) reverse[s] = p;
        return s == hash[p] && reverse[s] == p;
    });     
}
```

```JS
function solution(strings, patterns) {
    checkerPatterns = {}
    checkerStrings = {}
    
    
    for(i=0; i< strings.length; i++){
        
        // Check if pattern already occured
        if(checkerPatterns[patterns[i]]){
            if(checkerPatterns[patterns[i]] !== strings[i]){
                return false
            }
        } else{
            checkerPatterns[patterns[i]] = strings[i]
            console.log("word: " + strings[i] + " with new pattern: " + patterns[i] )
            
            // Check if word already occured
            if (checkerStrings[strings[i]]){
                console.log("word already exists")
                return false
            }
            
            checkerStrings[strings[i]] = true
        }
        
    }
    
    return true
}

```

# Check duplicates are close

```JS
function solution(nums, k) {

dic = {}

for(i=0; i< nums.length; i++){
    if(dic[nums[i]]){
        // Check range to last
        dif = i - dic[nums[i]][0]
        console.log(dif)
        if(dif <= k){
            return true
        } else{
            dic[nums[i]] = [i]
        }
    } else{
        dic[nums[i]] = [i]
    }
}

return false

}
```