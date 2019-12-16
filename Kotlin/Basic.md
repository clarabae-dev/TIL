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

#### Constants  
const val은 런타임에 할당되는 val과 달리 컴파일 시간에 결정되는 상수.  
문자열이나 기본 자료형만 할당이 가능하다.  
val은 const 없이는 Java Class가 호출할 수 있는 public으로 노출하지 않는다.  
val로 Java 스타일의 static final 변수를 선언하기 위해서는 @JvmField 키워드가 필요하다.  
@JvmField val로 선언한 프로퍼티는 Java Class에서도 호출할 수 있다.  
Kotlin Class에서 상수는 companion object 안에 const val로 선언한다.  

#### Any  
Java의 Object와 같은 최상위 객체(컴파일 시 Object로 변환)이지만,  
Java와 달리 Int, Boolean 등 원시 타입의 상위 객체이기도 하다.  
