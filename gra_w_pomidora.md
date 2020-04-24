# Gra w pomidora

Kojarzycie grę w pomidora? Zasady są proste -- jedna osoba mówi cokolwiek, a druga odpowiada na to *pomidor*. Kto pierwszy zacznie się śmiać -- przegrywa. ((Na warszawskim Mokotowie znana była inna wersja gry: przegrywał ten, który powiedział co innego niż *pomidor*.))

Smutek Podlasia przeniósł tę grę na komputer. Poniżej wersje na różne platformy.

The *pomidor* game is a simple game of polish children. One person says anything, and the other answers *pomidor* (in polish it means *tomato*). Whatever is the question, answer is always the same: *pomidor*. Yes, the game is quite strange, but children do play it.

The *Smutek Podlasia* art group made several implementations of this game in different programming languages. If you want create some other implementation, [contact us](zerro).

## BASH

Gra w pomidora w wersji dla GNU/Linuksa, powłoka bash((Tu warto zaznaczyć, że skryptów nieznanego pochodzenia (np. znalezionych w internecie) nie należy pod żadnym pozorem uruchamiać jako root -- mimo, że obrazek może sugerować co innego.)):

``` bash
$ echo "Gra w pomidora ver. 1.0"; while read; do echo "pomidor"; done
```

![filips:pomidor_lin.png](/.attachments/filips:pomidor_lin.png)

## sh (POSIX-1)

Gra w pomidora w wersji dla powłoki sh -- powinno więc działać w każdym środowisku zgodnym z POSIX-1:

``` bash
$ while read VAR; do echo "pomidor"; done
```

![pomidor-sh.png](/.attachments/pomidor-sh.png)

## Linia poleceń w Windows

Gra w pomidora w wersji dla Windows XP. Plik *pomidor.bat*:

``` bash
@echo off

echo Gra w pomidora ver. 1.0
:tutaj
set /p x=
echo pomidor
goto tutaj
```


![filips:pomidor_win.png](/.attachments/filips:pomidor_win.png)

## HTML

Gra w pomidora w wersji HTML. Plik *pomidor.html*:

``` html4strict
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN">

<html>
<head>
  <meta content="text/html; charset=iso-8859-2" http-equiv="Content-Type">
  <meta name="Author" content="good(k)night">
  <title>gra w pomidora w HTML</title>
  <style  TYPE="text/css">
  <!--
       p { color: #ff0000; padding-bottom: 2em }
       a img { border: 0 none; }
    -->
  </style>
</head>
<body>
<form action="">
<p>
Pomidor!<br>
<input type="text">
<input type="submit" value="ok">
</p>

<p>
<a href="http://validator.w3.org/check?uri=referer">
<img src="http://www.w3.org/Icons/valid-html401"
     alt="Valid HTML 4.01!" height="31" width="88">
</a>
</p>
</form>
</body>
</html>
```

## PHP

#### PHP/WWW

Gra w pomidora w wersji PHP. Plik *pomidor.php*:

``` php
<html>
 <head>
  <title>gra w pomidora w PHP</title>
  <meta name="author" content="Zerro">
  <meta content="text/html; charset=iso-8859-2" http-equiv=Content-Type>
 </head>

 <body topmargin="10" leftmargin="10">

<?
  if (isset($_POST['kaloryfer'])) {
    echo("<p>\nPomidor!\n</p>\n\n");
    $dialog=$_POST['dialog'] . "<br>\n" . "<font color=green>&gt; " . \
      $_POST['kaloryfer'] . "</font>" . \
      "<br><font color=red> &lt; Pomidor!</font><br>\n";
  } else {
    echo("<p>\nZagrajmy w pomidora. Powiedz coś\n</p>\n\n");  
    $dialog='';
  }
?>

    <form action="pomidor.php" method="POST">
      <input type=text name="kaloryfer">
      <input type=hidden name="dialog" value="<? echo $dialog ?>">
      <input type=submit value="ok">
    </form>

<hr>

<?
  echo($dialog);
?>

  </body>
</html>
```

![pomidor-php.png](/.attachments/pomidor-php.png)


#### PHP/CLI

Skrypt w PHP uruchamiany z linii poleceń.

``` php
#!/usr/bin/php -q

<?php

do {
    echo "Pytanie: ";
    $line = trim(fgets(STDIN));
    echo "Pomidor\n";
} while ($line!='');

?>
```

![pomidor-php-cli.png](/.attachments/pomidor-php-cli.png)

## Perl

Gra w pomidora w wersji perlowej:

``` bash
$ perl -pe 's/.*/pomidor/'
```

Skrinszot:

![filips:pomidor_perl.png](/.attachments/filips:pomidor_perl.png)

## Python

Gra w pomidora w wersji pythonowej:

``` python
#!/usr/bin/python

from sys import stdin

print "Gra w pomidora ver. 1.0"
while stdin.readline():
	print "pomidor"
```

## Common Lisp

Gra w pomidora w wersji common-lispowej:

``` lisp
(format t "Gra w pomidora ver. 1.0~%")
(do () (nil)
  (read-line)
  (format t "pomidor~%"))
```


## C

Gra w pomidora w wersji C:

``` c
#include <stdio.h>

int main() {
  printf("Gra w pomidora ver. 1.0\n");
  while (1) {
    if ( getchar() == '\n')
      printf("pomidor\n");
  }
  return 0;
}
```

## C++

Gra w pomidora w wersji C++:

``` cpp
#include <iostream>

#include <string>

using namespace std;

int main() {
  cout << "Gra w pomidora ver. 1.0" << endl;
  string x;
  while ( getline(cin, x) )
    cout << "pomidor" << endl;
  return 0;
}
```


## Moduł jądra dla Linuksa 2.6

Gra w pomidora jako moduł jądra dla linuksów z serii 2.6. 

### Pliki

Gra składa się z dwu plików:

*pomidor.c:*

``` c
#include <linux/module.h>

#include <linux/proc_fs.h>

static int pomidor_write(struct file *file, const char *buffer,
                   unsigned long count, void *data) {
        char buf[1024];
        copy_from_user(buf, buffer, count);
        buf[count]=0;
        printk("[pomidor]: ty < %s", buf);
        printk("[pomidor]: ja > pomidor\n");
        return count;
}

int init_module(void) {
        struct proc_dir_entry *proc_pomidor;
        printk("Modul pomidor zostal zaladowany.\n");
        proc_pomidor = create_proc_entry("pomidor", 0, 0);
        proc_pomidor->write_proc = pomidor_write;
        return 0;
}

void cleanup_module(void) {
        remove_proc_entry("pomidor", 0);
}
```

*Makefile:*

``` bash
bj-m += pomidor.o

all:
        make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules

clean:
        make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean
```

### Instrukcja obsługi

Aby zagrać w grę, należy:
 1.  skompilować moduł wydając polecenie *make*,
 2.  załadować moduł wydając (jako *root*) polecenie *insmod pomidor.ko*,
 3.  napisać coś do // /proc/pomidor//: *# echo Jak sie nazywasz? > /proc/pomidor *
 4.  obejrzeć logi kernela: *dmesg*.

Aha, uwaga: o ile kojarzę, żeby skompilować ten moduł, musisz mieć w katalogu // /usr/src/linux-wersja // aktualne źródła jądra. Ale jeśli masz w zwyczaju sam kompilować sobie jajko, to pewnie ten warunek masz spełniony.

### Skrinszoty

Zaczynamy od skompilowania i załadowania modułu:

![pomidor-mod-02.png](/.attachments/pomidor-mod-02.png)

Mówimy coś jądru -- a jądro na to: *pomidor!*:

![pomidor-mod-03.png](/.attachments/pomidor-mod-03.png)

I zaczyna się pyszna zabawa...

![pomidor-mod-04.png](/.attachments/pomidor-mod-04.png)


## VBA

Otwieramy edytor VBA (np w MS Excelu), wstawiamy nowy moduł w którym wpisujemy:

``` vba
Sub pomidor()
Dim q As String
Const a As String = "pomidor"
Const tytul As String = "Gra w pomidora"

Do
    q = InputBox("Pytanie?", tytul)
    MsgBox ("Q: " & q & Chr(13) & Chr(10) & "A: " & a)
Loop


End Sub
```

Skrinszoty:

![filips:pomidor_vba_q.png](/.attachments/filips:pomidor_vba_q.png)

![filips:pomidor_vba_a.png](/.attachments/filips:pomidor_vba_a.png)



## Matematyka

Gra w pomidora w wersji matematycznej:

*dla każdego x, p(x)=pomidor*


## Elektronika

Gra w pomidora zaimplementowana sprzętowo.

### Schemat

![pomidor-hw.png](/.attachments/pomidor-hw.png)

### Sposób montażu

Grę montujemy na płycie pilśniowej o rozmiarach 600x400 mm. W lewej jej części montujemy przełączniki *p1*-//p4// oznaczone plakietkami z napisami:

* dzień dobry,

* jak się nazywasz?,

* jak się miewasz?,

* co to jest -- zielone i skacze?,

W prawej części umieszczona jest żarówka *ż1* przykryta płytką z matowego pleksi z czerwonym napisem *pomidor*. 

### Instrukcja gry

Gracz wciska jeden z przycisków *p1*-//p4//, odpowiadający zadanemu pytaniu. W odpowiedzi automat zapala żaróweczkę, która podświetla udzieloną odpowiedź.

## Excel

Gra w pomidora w wersji excelowej:

![knight:pomidor-excel.png](/.attachments/knight:pomidor-excel.png)

W *D3* wpisujemy:

``` c
=JEŻELI(CZY.PUSTA(C3);"";"pomidor")
```

i kopujemy *D3* na obszar *D4:D10*.

## ekg2

Gra w pomidora w wersji dla [ekg2](http://dev.null.pl/ekg2/). W ekg2 wpisujemy polecenie:

    /on -a protocol-message 1 %1!==gg:<twoj_nr_gg> /chat "%1" pomidor

Teraz ktokolwiek do nas nie napisze, dostanie w odpowiedzi *pomidor*.

Zamiast powyższej, można też wpisać komendę:

    /on -a protocol-message 1 %1!==gg:<twoj_nr_gg> /^timer -a 2 /chat "%1" pomidor

Różnica jest taka, że odpowiedź *pomidor* będzie wysłana po dwóch sekundach od momentu otrzymania wiadomości, a nie od razu.


## asembler

; reaguje na ctrl-c``` asm
; używa funkcji DOS

.model small 
.386 

.data                     
   intro byte "Gra w pomidora ver. 1.0",0ah,0dh,"$"
   odp byte 0ah,0dh,"pomidor",0ah,0dh,"$"

.stack 100h  
.code  
   .startup 

	mov dx, offset intro   ; intro
	mov ah, 09h  
	int 21h 

poczatek:
	mov ah, 01h		; f-cja odczytu znaku z echem i ctrl-c
	int 21h

	cmp al, 0dh		; czy jest enter?
	jz koniec_wyp	; tak - odpowiedz
	jmp poczatek	; nie zczytujemy nastepny

koniec_wyp:
   mov dx, offset odp   ; odpowiedz
   mov ah, 09h  
   int 21h 
   jmp poczatek ;  

.exit

```
![pom1.gif](/.attachments/pom1.gif)

;nie reaguje na ctrl-c``` asm
; używa f-cji DOS-a

.model small 
.386 

.data                     
   intro byte "Gra w pomidora ver. 1.0.1",0ah,0dh,"$"
   odp byte 0ah,0dh,"pomidor",0ah,0dh,"$"

.stack 100h  
.code  
   .startup 

	mov dx, offset intro   ; intro
	mov ah, 09h  
	int 21h 

poczatek:
	mov ah, 07h		; f-cja odczytu znaku
	int 21h
	
	mov ah, 02h		; wyświetlanie
	mov dl, al
	int 21h

	cmp al, 0dh		; czy jest enter?
	jz koniec_wyp	; tak - odpowiedz
	jmp poczatek	; nie zczytujemy nastepny

koniec_wyp:
   mov dx, offset odp   ; odpowiedz
   mov ah, 09h  
   int 21h 
   jmp poczatek ;  

.exit

```

![pom2.gif](/.attachments/pom2.gif)

## Skrypt Matlab

function [] = pom()```
%% function[] = pom()
%% Gra w pomidora ver. 1.0

input('Gra w pomidora ver. 1.0\n','s');
while 1
    input('pomidor\n','s');
```


## Pascal

Gra w pomidora w wersji pascalowej:

``` pascal
PROGRAM Pomidor(INPUT,OUTPUT)

VAR
	ch	: CHAR;

BEGIN
	WRITELN('Gra w pomidora ver. 1.0');

	WHILE TRUE DO BEGIN
		WHILE NOT EOLN DO
			READ(ch);

		WRITELN;
		WRITELN('pomidor');
	END
END.
```



## C#

    (21:32:19) filips mówi: co to C# ?
    (21:32:53) mikus mówi: taki jezyk, cudenko techniki
    (21:33:03) mikus mówi: taka poprawiona Java, firmowana przez Microsoft  

``` c
using System;
namespace pomidor
{
/// <summary>
/// Klasa pomidora
/// </summary>
class Pomidor
{
 private static string line;
 /// <summary>
 /// Aplikacja realizuje znaną grę
 /// </summary>
 [STAThread]
 static void Main(string[] args)
 {
  while (true)
  {
   System.Console.WriteLine("pomidor");
   line = System.Console.ReadLine();
   System.Console.WriteLine("pomidor");
  }
 }
}
}
```


## Java Script

Gra w pomidora w javaskrypcie:

``` javascript
<html>
<head><meta http-equiv="refresh" content="6"></head>
<body>
<script type="text/javascript">
pytanie=prompt("","")
document.write("<font color=red>" + pytanie + 
  "</font><br><font color=green>" + "pomidor</font>")
</script>
</body>
</html>
```

## Atari Logo

```
TO POMIDOR
(PR [Gra w pomidora ver. 1.0]
REPEAT 65535 [RL PR[pomidor]])
END
```

## FORTRAN

``` fortran
! Gra w POMIDORA

       PROGRAM pomidor
       
       CHARACTER tekst*1000

       print *,'Gra w pomidora, ver.1.0'
       
  100  read *, tekst
       print *,'pomidor'
       GOTO 100

       END
```

## XSLT

Gra w pomidora w wersji XSLT. Na wejsciu prosze podać dowolny XML z pytaniem.

``` xml
<?xml version="1.0" encoding="utf-8"?>
<xs:stylesheet version="1.0" xmlns:xs="http://www.w3.org/1999/XSL/Transform">
    <xs:template match="*">
	<odpowiedz>pomidor</odpowiedz>
    </xs:template>
</xs:stylesheet>
```

Dokument wejściowy:

``` xml
<?xml version="1.0" encoding="utf-8"?>
<pytanie>Co dzis na obiad?</pytanie>
```

Wynik:

``` xml
<?xml version="1.0" encoding="utf-8"?>
<odpowiedz>pomidor</odpowiedz>
```

Wersja druga -- XSLT dla większej liczby pytań:

``` xml
<?xml version="1.0" encoding="utf-8"?>
<xs:stylesheet version="1.0" xmlns:xs="http://www.w3.org/1999/XSL/Transform">
    <xs:output encoding="utf-8" />
    <xs:template match="/*">
	<odpowiedzi>
	    <xs:apply-templates />
	</odpowiedzi>
    </xs:template>
    <xs:template match="*">
	<odpowiedz>pomidor</odpowiedz>
    </xs:template>
</xs:stylesheet>
```

Dokument wejściowy:

``` xml
<?xml version="1.0" encoding="utf-8"?>
<pytania>
    <pytanie>Gdzie jestes?</pytanie>
    <pytanie>Jak sie nazywasz?</pytanie>
    <pytanie>O co chodzi?</pytanie>
</pytania>
```

Wynik:

``` xml
<?xml version="1.0" encoding="utf-8"?>
<odpowiedzi>
    <odpowiedz>pomidor</odpowiedz>
    <odpowiedz>pomidor</odpowiedz>
    <odpowiedz>pomidor</odpowiedz>
</odpowiedzi>
```


## Delphi

``` xml
program Pomidor;

uses
  Dialogs;

begin
  repeat
    InputBox('Pytanie', 'Podaj pytanie:', '');
    ShowMessage('Pomidor');
  until False;
end.
```

## Prolog


### kod

``` prolog
% implementacja w GNU-prologu:
% /Dreamer_
get_line :- ( get_char('\n') ; get_line ).

play :-
        get_line,
        write('pomidor!'), nl,
        play.

pomidor :-
        write('Gra w pomidora ver. 1.0'), nl,
        play.
```

### sposób użycia

Niech program będzie zapisany w pliku *pom.pl*. Po uruchomieniu GNU-prologa wpisujemy:
```
| ?- [pom].
| ?- pomidor.
```

## Haskell

``` haskell
import IO

pomidor = do
        putStrLn "Gra w pomidora ver. 1.0"
        play where
                play = do
                        getLine
                        putStrLn "pomidor!"
                        play
```

## Ruby

``` ruby
ruby -n -e 'print "pomidor\n"'
```

## Ocaml

``` ocaml
let _ = 
  while true do 
    let _ = read_line () in 
    let _ = print_string "pomidor\n" in 
    () 
  done
```

## Brainfuck

``` brainfuck
+[[,----------]>+++++++++++[<++++++++++>-]<++.-.--.----.-----.+++++++++++.
+++.[-]++++++++++.]
```

## Focal

Z Wikipedii: Largely the creation of Richard Merrill, FOCAL was initially written for and had its largest impact on the Digital Equipment Corporation's (DEC's) PDP-8 computers. Merrill wrote the original (1968) and classic FOCAL-69 interpreters for the PDP-8. Digital itself described FOCAL as "a JOSS-like language."

Like early versions of BASIC, FOCAL was a complete programming environment in itself, requiring no operating system. As in MUMPS, most commands could be, and in practice were, abbreviated to a single letter of the alphabet. Creative choices of words were used to make each command uniquely defined by its leading character. Digital made available several European-language versions in which the command words were translated into the target language.

Więcej: http://en.wikipedia.org/wiki/FOCAL_programming_language

##### Przygotowanie

 1.  Bierzemy dowolnego linuxa
 2.  Ściągamy pakiet http://www.pdc.kth.se/~jas/retro/focal.tar.gz
 3.  Rozpakowujemy
 4.  Kompilujemy: ``make``. Otrzymujemy plik wykonywalny ``focal``
- Przygotowujemy plik ''pomidor.foc'':``` focal
01.10 ASK "PYTANIE", PYT
01.20 TYPE "POMIDOR!",!
02.10 GOTO 01.10
```
 5.  uruchamiamy interpreter ``focal``
 6.  wczytujemy nasz program: ``lib call pomidor.foc``
 7.  uruchamiamy ``go``
 8.  bawimy się do upadłego

![pomidor-focal.png](/.attachments/pomidor-focal.png)

 --- //[Filip Stefaniak] 2006-09-07 16:40//

## QBASIC (zawarty w MS DOS 6.22)

``` basic
1 INPUT text$
2 PRINT "POMIDOR"
3 GOTO 1
4 END
```

## Basic dla Atari/C64

``` basic
10 REM kod należy przepisać i ewentualnie nagrać na kasetę w Atari/Commodore itd
20 print pomidor ver 1.0
30 input $a
40 print pomidor
50 goto 30
```


## Multimedialna gra w pomidora

Do uruchomienia gry potrzebne są: *Sound eXchange (sox)*, *bash*,
działające urządzenie */dev/dsp* z uprawnieniami do zapisu i odczytu,
mikrofon oraz słuchawka.

1. Podłączamy mikrofon oraz słuchawkę do odpowiednich złącz w karcie dźwiękowej.

2. W mikserze karty dzwiekowej ustawiamy przechwytywanie dźwięku z
mikrofonu oraz regulujemy poziom zapisu.

3. Tworzymy plik dżwiękowy o nazwie "pomidor".

``` bash
$ rec -c 1 -f u -r 8000 -s b -t raw pomidor
```

następnie mówimy do mikrofonu "pomidor" i kończymy nagrywanie
wciskając [CTRL]+[C]

4. Startujemy grę:

``` bash
while true; clear; do rec -r 8000 -t raw /dev/null silence 1 1 20%
30 100 5% > /dev/null; echo -e "    V\n  x.|.x\n #.   .#\n{#     #}\n
#.   .#\n  x.'.x"; cat pomidor > /dev/dsp; done

```

Uwaga: pierwsze trzy parametry po silence opisują parametry
odblokowania bramki szumowej, a kolejne trzy odpowiadają za opoznienie
i poziom dźwięku, przy którym bramka się zamyka. Nalezy je
ekseperymentalnie dobrac do poziomu zapisu dźwięku w karcie
dźwiękowej. Więcej informacji w manualu *sox*.

5. Mówimy do mikrofonu, a komputer odpowiada nam na wyszstkie
Ostateczne Pytania o Życie, Wszechświat i całą resztę.

## Shell AmigaDOS i MorphOS (klon AmigaOS)

```
echo "Gra w pomidora, wersja 1.0 dla AmigaDOS/MorphOS Shell."
lab start
echo noline "> "
set >nil: temp ?
echo "pomidor"
skip start back
```

![pomidor-morphos.png](/.attachments/pomidor-morphos.png)

*nadesłał Marek Szyprowski*


## JAVA

``` java
/*

 * Main.java
 * @author SOCAR http://www.socar.xt.pl
 *
 */

package pomidor;
import java.io.BufferedReader;
import java.io.InputStreamReader;

public class Main {
    
   
    public Main() {}
    
    /**

     * @param args the command line arguments
     */
    public static void main(String[] args) {
               
        boolean goaway=false;
        try{
        while(!goaway)
        {      
            new BufferedReader(new InputStreamReader(System.in)).readLine();
             System.out.println("Pomidor");              
        }
        
        
    }catch(Exception e){System.out.println("Nie mam pojecia co zrobiles zle :/");};
    }
    
}

```

## Clojure 1.0

``` clojure
(loop [] 
  (read-line) 
  (print "pomidor\n") 
  (flush) 
  (recur))
```

# Pomidor w różnych językach

Przewidując konieczność internacjonalizacji gry w pomidora uważam, że należy stworzyć listę słowa *pomidor* w różnych językach:


* polski / polski / polish -- pomidor

* angielski / english / english -- tomato

* nowogrecki -- domata

* greka starożytna -- chrysomilo ((Tak, wiemy, że starożytni Grecy nie znali pomidorów, ale jednak... gdyby jednak go znali, to jakby go nazywali? Kolega P. Kordos powiedział: *Właśnie mi się przypomniało, że na fali puryzmu Grecy zrobili taką starogrecką formę. Kalkuje etymologię z francuskiego i brzmi chrysomilo, czyli złote jabłko. *))
