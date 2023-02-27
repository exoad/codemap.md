# Jack's Universal Code Syntax Format

## Table of Contents

* ### [**Preface**](#Preface)
* ### [**Comparison**](#Comparison)

## Preface
Notice: This document covers general ideas around syntax formatting and does not dive deeply into any specific language(s). If you would like to check out individual languages and how they inherit these guidelines, head over to their individual folders.

This syntax and format is not for a person who has minimal or grasp on a language/toolkit OR for writing code that is not meant to be read by a human. For a beginner, it is recommended to learn the fundamentals before adopting this styling in order to understand how to PROPERLY order certain structures, follow lexical scoping, and allowed syntax.

General ideas covered include those that can be found in all languages that are commonly used:
* Naming Conventions
* Brackets Styling
* Condensing & Inlining

## Comparison
Here is a simple comparison of some C code aligned with standard conventions versus that of the improved conventions (this documentation).

**Standard Conventions** (*)[^1]
```c
#include <stdio.h>

struct Exoad
{
	int id;
	char name[256];
	double score;
}

void set_vals(Exoad *ex, int id, char *name, double score)
{
	asm volatile(		"mov %[id], %[ex_id]\n\t"
		"mov %[name], %[ex_name]\n\t"
		"movsd %[score], %[ex_score]\n\t":[ex_id]
		"=r"(ex->id),
	[ex_name]
		"=r"(ex->name),
	[ex_score]
		"=t"(ex->score):[id]
		"r"(id),
	[name]
		"r"(name),
	[score]
		"t"(score)
);
}

int main()
{
	Exoad ex;
	register int id asm("ebx") = 123;
	register char *name asm("ecx") = "Jack Meng";
	register double score asm("xmm0") = 3.1415;
	set_vals(&ex, id, name, score);
	printf("ID: %d\n", ex.id);
	printf("Name: %s\n", ex.name);
	printf("Score: %f\n", ex.score);
}
```

**Improved Conventions**

```c
#include <stdio.h>

struct Exoad 
{ int id;
  char name[256];
  double score; }

void 
set_vals(Exoad *ex, int id, char *name, double score)
{
    asm volatile (
        "mov %[id], %[ex_id]\n\t"
        "mov %[name], %[ex_name]\n\t"
        "movsd %[score], %[ex_score]\n\t"
        : [ex_id] "=r" (ex->id),
          [ex_name] "=r" (ex->name),
          [ex_score] "=t" (ex->score)
        : [id] "r" (id),
          [name] "r" (name),
          [score] "t" (score)
    );
}

int
main()
{
    Exoad ex;
    register int id asm("ebx") = 123;
    register char *name asm("ecx") = "Jack Meng";
    register double score asm ("xmm0") = 3.1415;
    set_vals(
        &ex,
        id,
        name, 
        score
    );
    printf("ID: %d\n", ex.id);
    printf("Name: %s\n", ex.name);
    printf("Score: %f\n", ex.score);
}
```

You might notice that there is not a lot of difference, but this is because with the limited range of definable structures in C, it is often very sparse for this formatting guide to work. But overall, for a sparse language like C, it is not as necessary to use this formatting guide.

## Footnotes
[^1]: This is just a common way for most programmers to format their code, it should not be taken as the "standard standard" way to format that language's code.