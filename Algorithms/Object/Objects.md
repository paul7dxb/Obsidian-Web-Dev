# Iterate through object

```JS
function solution(shoes) {
    
    const dic = {}
    
    for (let shoe of shoes){
        if (!dic[shoe[1]]){
            dic[shoe[1]] = {}
            if(shoe[0]){
                dic[shoe[1]].right = 1
            } else{
                dic[shoe[1]].left = 1
            }
        } else{
             if(shoe[0]){
                dic[shoe[1]].right = dic[shoe[1]].right ?  dic[shoe[1]].right + 1 : 1
            } else{
                dic[shoe[1]].left = dic[shoe[1]].left ? dic[shoe[1]].left + 1 : 1
            }
        }
    }
    
    for(let size in dic){
        console.log(size)
        if(dic[size].left !== dic[size].right){
            return false
        }
    }
    
    return true
    
}
```