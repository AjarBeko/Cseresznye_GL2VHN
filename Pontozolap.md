# Software Engineering CherryPicking
##  Adatbázis leírása
Az adatbázis tartalma három tábla, amelyek ügyfeleket tart nyilván, a lakcímükkel és a hozzájuk tartozó autókkal együtt. A táblák összetétele: az "AUTO" tábla autókat tartalmaz, amelyben meg van jelenítve az adott autó gyártási éve, márkája, modell neve, kivitele, illetve az ID-k amelyek, összekötik az ügyfél táblával. A második tábla az ügyfeleket jeleníti meg, elnevezése "UGYFEL", mindannyiuk külön ID-val rendelkeznek a könnyű azonosítás érdekében. Ezentúl itt szerepel a nevük, e-mail címük, telefonszámuk, lakcimID és AutoID. Utóbbi kettő tábla az " CIM ", illetve a "AUTO" táblákkal való kapcsolódást segíti. Az utolsó tábla pedig a "CIM" tábla névre hallgat. Itt szerepelnek az ügyfelek lakcímei, ország, város, irányítószám, utca, illetve házszámmal ellátva. Ezen felül az összeköttetéshez elengedhetetlen CimID szerepel ebben a táblában.
## Hozott anyagok
Az adatbázis saját Azure szerveren helyezkedik el.
![image](https://github.com/user-attachments/assets/59446f64-4797-4abd-9373-0e31439764f9)
![image](https://github.com/user-attachments/assets/fff78150-de60-4048-b3ce-22ecda9158e4)
![image](https://github.com/user-attachments/assets/2e16c2c9-a021-4028-b5c6-881410a546bd)
![image](https://github.com/user-attachments/assets/2d80c584-14da-4152-a5ca-ef13643cb873)

Az adatbázishoz az SQL-t egy C# scripttel generáltam a ChatGPT-nek beadott promptok álta, majd a scripteket lefuttattam Azure Data studio-ban. Ehhez tartozik egy Scaffold-DbContext, amellyel tudunk csatlakozni az adatbázishoz az API-val és a Form-mal. A promptok és a Scaffold-DbContext itt találhatók. 
-	3x1p Az alkalmazásban használt táblánként pont (Ugyfelek, Cimek, Autok)
-	1p Az adatbázis tartalmaz Constraint-eket (min 2)
-	2p Az adatbázis saját Azure SQL szerveren van
-	1p Az adatbázis adatainak forrásmegjelölése értsd: miből készült és hogyan(itt)
-	2x1p Scaffold-DbContext használata (ajándék)
### ASP .NET
Ehhez az adatbázishoz nem tartozik kész, adatokkal feltöltött weblap, csupán egy kész css, ami csak arra vár, hogy fel legyen töltve tartalommal.
- 1p A weboldal használ legalább 20 sor értelmes css-t
A program.cs-ben el lett helyezve kettő új sor, amelyek a statikus tartalmak megosztására szolgálnak
-	app.UseDefaultFiles();
-	app.UseStaticFiles();
-	1x2p program.cs beállítása wwwroot mappában tárolt statikus tartalmak megosztására
Létre lett hozva egy új controller, amelyben API végpontokon keresztül az egész SQL táblát elérjük. Ezentúl lehet hozzáadni, törölni mindegyik táblából, HttpPost, illetve HttpDelete kódon keresztül. (DatabaseController.cs)
-	1x3p Teljes SQL tábla adatainak szolgáltatása API végponton keresztül
-	2x2p SQL tábla egy választható rekordjának szolgáltatása API végponton keresztül
-	1x3p SQL tábla egy választható rekordjának törlése
-	1x5p Új rekord felvétele HttpPost metóduson keresztül SQL táblába
![image](https://github.com/user-attachments/assets/d3e55c6e-c7d4-4e1a-9fe1-8329ca39cc5a)
### Windows Forms Application
A futtatáskor egy fő oldalt látunk, ahonnan három UserControl-on keresztül tudjuk elérni az adatbázis tábláit. Ha kiszeretnénk lépni az alkalmazásból, akkor azt csak egy megerősítést követően tudjuk megtenni (Form1.cs). Ezen felül az ablakok tartalmaznak Anchorokat, hogy az átméretezéskor is minden elem megfelelően látszodjon.
-	1x2p Az alkalmazásból a kilépés csak megerősítő kérdés után lehetséges.
-	3x2p Olyan alkalmazás elrendezés, melyben gombok lenyomására UserControl-ok kerülnek elhelyezésre egy Panel vezérlőben, teljesen kitöltve azt. Minden gombra jár a pont, amennyiben az funckuonlalitással rendelkező UserControl-t tölt be.
-	1x2p Anchorok alkalmazása: az alkalmazás egészében meg van oldva, hogy az ablak átméretezésekor ki legyen használva a rendelkezésre álló terület. 
![image](https://github.com/user-attachments/assets/5ee10dfb-c695-4c5a-ad0e-5e502acb89a4)
![image](https://github.com/user-attachments/assets/d1461026-c807-4646-804e-9324a0351db3)
#### UserControl1
Az első UserControl-ban az ügyfelek listázása történik ListBox-ban, ahol egy textbox-on keresztül tudunk szűrni a kívánt névre. Illetve az éppen aktuálisan kiválasztott nevet törölni is tudjuk az adatbázisból (UserControl1).
-	1x2p Adatok megjelenítése
-	2x2p Ha az adatok tetszőleges módszerrel, pl. TextBox-on keresztül szűrhetőek.
![image](https://github.com/user-attachments/assets/52cd141a-8ec3-41df-9fc4-14eee3d939a5)
![image](https://github.com/user-attachments/assets/8ee35484-7b48-4265-9574-56bbdc8fed0b)
#### UserControl2
A második UserControl-ban DataGridView-n keresztül jelentjük meg az Ügyfeleket. Itt tudunk felugró ablakon keresztül új ügyfelet hozzáadni, illetve a kiválasztott ügyfél adatait tudjuk módosítani, szintén egy felugró ablakon keresztül. Az adatok hozzáadásához erős validáció is tartozik, annak érdekében, hogy az adatbázisban ne szerepeljen hibás formátumú adat (regex, errorprovider). Ezentúl itt is tudjuk törölni az aktuálisan kiválasztott adatot.
•	1x2p Adatok megjelenítése
-	3x1p Többablakos alkalmazás legalább két felugró ablakkal. Minden Form-nak saját osztályon kell alapulnia, és funcionalitással kell rendelkeznie. Az ablakok nyílhatnak gombokkal vagy felső menüből is.
-	1x1p Ha legalább egy nem kulcs mező, pl. Mennyiség is fel van véve
-	1x2p Felugró ablakon keresztül történik Ok és Mégse gombbal
-	2x1p A kitöltési hiba ErrorProvider-en keresztül kerülnek köközlésre a felhasználóval, hibás kitöltés esetén nem enged rányomni az Ok gombra
-	1x2p Regex alapú validáció
-	1x1p Hibás kitöltés esetén nem lehet megynomni az Ok gombot.
-	1x2p Sikeres törlés
-	1x2p Megerősítéshez kötött törlés
![image](https://github.com/user-attachments/assets/5cfe9f8b-d0cc-42cb-b22f-8020f400cbd3)
![image](https://github.com/user-attachments/assets/3c9bea10-b2e3-46ca-bb47-6b77dd284922)
![image](https://github.com/user-attachments/assets/24c7a5a6-f79d-4872-9942-0a0e596250ac)
![image](https://github.com/user-attachments/assets/ed6aa892-8efe-46ba-ad04-f0118204d26a)
#### UserControl3
A harmadik UserControl-ban DataGridView-ban megjelenítésre kerülnek a gépjárművek, és hozzá tartozik két számítás. Az egykben az adatbázisban szereplő autók számát írjuk ki, a másodikban, pedig az átlagos hengerűrtartalmat, amivel az autók rendelkeznek.
-	1x2p Adatok megjelenítése
-	1x1p Az algoritmus (8. osztályig nem tanított) matematikai képletet is alkalmaz
![image](https://github.com/user-attachments/assets/4e0a6365-0d88-4a3f-a04b-c3e00285afa5)
#### Adatkötés BindingSource-on keresztül
-	1x2p Működő BindingSource
-	3x1p Egy BindingSource-ra egy gyűjemény megjelenítésére alkalmas vezérlő (ListBox, ComboBox, DataGridVIew) mellett más adatkötött vezérlő is van kötve, mint TextBox, DateTimePicker, ComboBox idegen kulcs értékének beállítására, stb.
![image](https://github.com/user-attachments/assets/28fa8b86-d2bc-414e-aa7a-fe436f0fe25b)
![image](https://github.com/user-attachments/assets/c7db2047-87a4-4d5c-aa62-57a2db49d07a)

