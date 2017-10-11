# 3장 함수와 프로그램 구조 

## 3.1 기본함수 

### 기본함수의 형태 
<pre><code>
반환타입 함수명(매개변수)
{
	선언 및 상태
}
</code></pre>

<pre><code>
/*getline함수 : 문자열 s의 길이를 반환하는 함수 */

int getline(char s[], int lim)
{
	int c, i;

	i= 0;

	while(--lim > 0 && (c=getchar()) != EOF && c != '\n')
	{
		s[i++] = c;
	}
	if(c == '\n')
	{
		s[i++] = c;
	}
	
	s[i] = '\0';
	return i;
}
</code></pre>

## 3.2 반환타입이 정수가 아닌 함수들 

### atof함수: 문자열 s를 더블타입으로 변환 하는 함수 

<pre><code>

double atof(char s[])
{
	double val, power;
	int i, sign;

	for(i=0; isspace(s[i]); i++)
		;
	sign = (s[i] == '-') ? -1:1;
	if(s[i] == '+' || s[i] == '-')
	{
		i++;
	}
	for( val = 0.0; isdigit(s[i]); i++)
	{
		val = 10.0 * val +(s[i] - '0');
	}
	if(s[i] == '.')
	{
		i++;
	}
	for( power = 1.0; isdigit(s[i]); i++)
	{
		val = 10.0 * val + (s[i] - '0');
		pwoer *= 10;
	}

	return sign * val / power;
}

</code></pre>

## 3.3 외부변수 
함수 밖에 선언되는 변수이다.
다른 여러 함수들이 사용할 수 있고 다른 파일에서도 외부변수를 사용할 수 있다.


## 3.4 정의한 변수의 영향범위 

## 3.5 헤더파일 

## 3.6 정적변수 
일반 변수는 프로그램이 끝나면 변수의 메모리공간이 사라지지만, 
정적변수(static)는 프로그램이 종료되도 메모리 공간에 그대로 존재한다.

<pre><code>
void add(void);

int main()
{
	add();
	add();

	return 0;
}


void add()
{
	static int i = 0;
	i+= 10;
	printf("Value of i : %d\n", i);
}
</code></pre>

## 3.7 레지스터 변수
레지스터 변수는 CPU의 레지스터에 위치하여 빠르게 처리가 가능하다.

<pre><code>
register int x;
register char c;

void f(register unsigned m, register long n)
{
	register int i;
	...
}
</code></pre>


## 3.8 블록구조 
C언어에서는 함수에 안에 다른 함수를 정의할 수 없다(즉 C언어는 블록구조 언어가 아니다).
하지만 변수는 함수안에 블록구조 형식으로 정의될 수 있다.
아래의 구조 처럼 if문안에 있는 i와 if문블록 외부의 변수i와는 관계가 없다.

<pre><code>
int i = 10;

if(n>0)
{
	int i;

	for(i=0; i<n; i++)
	{
		...
	}
}
</code></pre>

아래의 코드도 동일한 형태이다.
함수 f안에 있는 x,y는 함수외부의 변수와는 별개이다. 

<pre><code>
int x;
int y;

void f(double x)
{
	double y;
}

</code></pre>


## 3.9 초기화 
<pre><code>
int binsearch(int x, int v[], int n)
{
	int low = 0;
	int high = n-1;
	int mid;
	...
}

/*위의 표현은 원래아래의 부분을 간결하게 하였다
코드를 보기 쉽고 이해하기 쉽게 표현하는 것이 좋다.*/

int low, high, mid;

low = 0;
high = n-1;
</code></pre>

## 3.10 재귀함수 
c 함수는 직,간접적으로 자기자신 호출이 가능하다.

재귀함수 사용조건은  반복을 끝내는 조건이 있어야 한다.
만약 끝나는 조건이 없다면 끝없이 함수를 계속 호출 하기때문에, 
Overflow가 일어날수있다.

<pre><code>
/*printd 함수 : n를 10진수로 출력하는 함수 */

void printd(int n)
{
	if(n < 0)
	{
		puchar('-);
		n = -n;
	}
	if(n/10)
	{
		printd(n/10);
	}
	puchar(n % 10 + '0');
}
</code></pre>


## 3.11 C 전처리기 
C 전처리기(프리프로세스)는 컴파일 하기 전 처리단계이다.
가장 자주 사용되는 두가지 기능은 특정 함수들이 들어가 있는 파일을 포함하는 #include와 
임의의 문자를 대응하는 문자열로 치환하는 #define이 있다.

### 3.11.1 파일삽입
특정 파일을 해당 프로그램에서 사용하고자 할때 사용한다.
<pre><code>#include "filename" #include <filename>
</code></pre>

### 3.11.2 메크로 치환 
특정 문자를 매크로 이름으로 바꾸어 컴파일한다.
긴숫자나, 문자를 명확하고 간결하게 할 수 있다.

형태 #define 대체될이름 본래의내용 
우리가 3.14159라는 숫자를 PI라고 하는 것과 같다
<pre><code>#define PI 3.14159
</code></pre>

아래의 역할을 수행하기도 한다.
<pre><code>
#define mac(A,B) ((A) > (B) ? (A): (B))

x = max(p+q, r+s);
/*x = ((p+q) > (r+s) ? (p+q) : (r+s));와 같은 내용*/

</code></pre>

그리고 #undef명령에 의해 선언했던 내용이 해제될 수 있다
<pre><code>#undef identifier
</code></pre>



