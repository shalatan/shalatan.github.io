## Table of contents
- [Array](#arrays)
- [Loop](#loop) 

## Arrays
- `Array<Int>` is an Integer[], means it will be boxed with Integer.parseInt()
- `IntArray` is an int[], in it no boxing will occur, becuase it translates to Java primitive array.
    - val arr = IntArray(10)
    - val arr = intArrayOf(1,2,3,4,5)

## HashSet
```kotlin
var hashSet = hashSetOf<Int>()
var hashSet = hashSetOf<Int>(1,2,3,4,5,6)
var hashSet: HashSet<String> = hashSetOf<String>()
val mySet = setOf(6,4,29)

// putting into hashSet
hashSet.add(item)
hashSet.addAll(mySet)

// checking
hashSet.contains(item)
hashSet.containsAll(mySet)

// removing
hashSet.remove(item)
hashSet.removeAll(mySet)

// traverssing hashSet
for(item in hashSet){

}

// misc
hashSet.isEmpty()
hashSet.isNotEmpty()
hashSet.clear()
hashSet.size
```

## HashMap
```kotlin
var hashMap: HashMap<String,Int>= HashMap<String,Int>()

// printing hashmap
print(hashMap)

// putting into hashmap
hashMap.put("IronMan", 3000)
hashmap["IronMan"] = 3000
hashMap.replace("IronMan",99) // for updating

// getting from hashmap
hashMap.get(key)

// traverssing hashmap keys
for(key in hashmap.keys){

// misc
hashMap.size
hashMap.isEmpty()
hashMap.clear()
hashMap.containsKey(key)
hashMap.containsValue(value)
hashMap.remove(key)
}
```
## Loop
```kotlin
- val nums = {1,2,3,4,5}
- for(num in nums) l̥
    : 1,2,3,4,5
- for(i in nums.indices)
    : 0,1,2,3,4
- for(i in 1..5)
    : 1,2,3,4,5
- for(i in 5 downTo 1)
    : 5,4,3,2,1
- for(i in 1..5 step 2)
    : 1,3,5

- val text = "kotlin"
- for(letter in text)
    : k,o,t,l,i,n
- for(i in text.indices)
    : 0,1,2,3,4
```