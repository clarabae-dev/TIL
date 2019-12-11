#### Functions
Function with an expression body and inferred return type.  
fun sum(a: Int, b: Int) = a + b  

#### Strings
1. Strings are immutable. Elements of a string are characters that can be accessed by the indexing operation: s[i].  
for (c in str) {  
    println(c)  
}  

2. Concatenate strings using the + operator.  
This also works for concatenating strings with values of other types, as long as the first element in the expression is a string.  
val s = "abc" + 1  
println(s + "def")  
//abc1def  

3. Template  
var a = 1  
val s1 = "a is $a"// simple name in template:  
a = 2  
// arbitrary expression in template:  
println("${s1.replace("is", "was")}, but now is $a")  
// a was 1, but now is 2  

#### Control Flow
1. If Expression  
- There is no ternary operator (condition ? then : else).  
val max = if (a > b) a else b  

- if branches can be blocks, and the last expression is the value of a block.  
val max = if (a > b) {  
    print("Choose a")  
    a  
} else {  
    print("Choose b")  
    b  
}  

2. When Expression
- when replaces the switch operator.  
when matches its argument against all branches sequentially until some branch condition is satisfied.  
when (x) {  
    1 -> print("x == 1")  
    2 -> print("x == 2")  
    else -> { // Note the block  
        print("x is neither 1 nor 2")  
    }  
}  

- If many cases should be handled in the same way, the branch conditions may be combined with a comma.  
when (x) {  
    0, 1 -> print("x == 0 or x == 1")  
    else -> print("otherwise")  
}  

- Can use arbitrary expressions (not only constants) as branch conditions.  
when (x) {  
    parseInt(s) -> print("s encodes x")  
    else -> print("s does not encode x")  
}  

- Can also check a value for being in or !in a range or a collection.  
when (x) {  
    in 1..10 -> print("x is in the range")  
    in validNumbers -> print("x is valid")  
    !in 10..20 -> print("x is outside the range")  
    else -> print("none of the above")  
}  

- Check that a value is or !is of a particular type. Due to Smart Casts.  
fun hasPrefix(x: Any) = when(x) {  
    is String -> x.startsWith("prefix")  
    else -> false  
}  

- Since Kotlin 1.3, it is possible to capture when subject in a variable.  
Scope of variable, introduced in when subject, is restricted to when body.  
fun Request.getBody() =  
    when (val response = executeRequest()) {  
        is Success -> response.body  
        is HttpError -> throw HttpException(response.status)  
    }  

#### Data Class
data class  
dto 또는 vo class를 선언하는 기본 방식이다.  
생성자 파라미터로 프로퍼티들을 선언할 수 있다.  
val: private, getter  
var: private, getter, setter  
