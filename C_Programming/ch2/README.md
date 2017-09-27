# 2장 제어흐름 

## 2.1 상태와 블록

<pre><code> x = 0; i++ printf(...); </code></pre>

## 2.2 If-Else문
<pre><code>
if(expression)
{
	statemet1
}
else
{
	statement2
}

if (n>0)
{
	if(a>b)
	{
		x =a;
	}
	else
	{
		z = b;
	}
}
</code></pre>

## 2.3 Else-If문
<pre><code>
if (expression)
{
	statement
}
else if (expression)
{
	statement
}
eles
{
	statement
}
</code></pre>

## 2.4 Switch문 
<pre><code>
switch(expression)
{
	case const-expr: statement
	case const-expr: statement
	default: statemetns
}
</code></pre>

## 2.5 반복문- While and For문
<pre><code>
while (expression)
{
	statement
}

for (expre1; expr2; expr3)
{
	statement
}
</code></pre>

## 2.6 반복문 - Do-While
<pre><code>
do
{	
	statement
}
while(expression);
</code></pre>


## 2.7 Break and Continue
<pre><code> 
for(statement1; statement2; statement3)
{
	if(statement)
	{
		`break;`
	}
}

for(statement1; statement2; satement3)
{
	if(statement)
	{
		`continue`
		/*if문의 참이면 실행하라 */
	}
}
</code></pre>

## 2.8 Goto

<pre><code>
if(disaster)
{
	goto error;
}
error: /* clean up the mess*/
</code></pre>

