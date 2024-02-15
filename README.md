Popis úlohy
Česká kontrarozvědka FDTO (Fakt Děsně Tajná Organizace) má podezření, že v jejích řadách působí krtek a služba tak byla kompromitována. Obsah některých přísně tajných digitálních dokumentů byl nejenže vyzrazen tajným službám cizích mocností, ale zřejmě i modifikován, což způsobilo chaos v organizaci některých tajných operací a částečně tak paralyzovalo fungování celé kontrarozvědky. V zájmu národní bezpečnosti je zapotřebí krtka urychleně najít a polapit. Hledání však musí být maximálně diskrétní, aby krtek netušil, že se okolo něj utahuje smyčka.

Protože zavedení nových oficiálních bezpečnostních opatření při práci s utajovanými digitálními dokumenty by mohlo být podezřelé a krtka vyplašit, rozhodlo se vedení kontrarozvědky, že bude potřeba tato bezpečností opatření zavést utajeně. Tedy tak, aby si nikdo (kromě nejužšího vedení a Vás) nebyl vědom toho, že nějaká nová opatření vešla v platnost.

Vzhledem k Vaší léty prověřené loajalitě a bezchybné pracovní historii v IT jednotce kontrarozvědky jste byli pro tuto tajnou misi vybráni právě Vy. Vaším úkolem je vytvořit skript, který bude prezentován jako nový interní nástroj pro zvýšení efektivity při práci s elektronickými dokumenty, zatímco skrytě bude použit pro tajné zaznamenávání (tzv. logging) a ohlašování informací o tom, se kterými dokumenty (a kdy) daný uživatel pracoval.

Citlivé dokumenty jsou v kontrarozvědce zásadně uchovávány na serverech a přístup k nim probíhá vzdáleně pomocí příslušných nástrojů. Skript mole (Makes One’s Life Easier) tedy bude fungovat jako tzv. wrapper nad textovými editory, což znamená, že textový editor bude spouštěn skrze skript mole. Skript si bude pamatovat, které soubory byly v jakém adresáři prostřednictvím skriptu mole editovány. Jednotlivé soubory je zároveň možné přiřazovat do skupin pro jednodušší filtrování při práci s velkým množstvím souborů. Pokud bude skript spuštěn bez parametrů, vybere skript soubor, který má být editován.

Specifikace chování skriptu
JMÉNO

mole – wrapper pro efektivní použití textového editoru s možností automatického výběru nejčastěji či posledně modifikovaného souboru.
POUŽITÍ

mole -h
mole [-g GROUP] FILE
mole [-m] [FILTERS] [DIRECTORY]
mole list [FILTERS] [DIRECTORY]
mole secret-log [-b DATE] [-a DATE] [DIRECTORY1 [DIRECTORY2 [...]]]
Popis
-h – Vypíše nápovědu k použití skriptu (volba secret-log by neměla být v nápovědě uvedena; nechceme krtka upozornit, že sbíráme informace).
mole [-g GROUP] FILE – Zadaný soubor bude otevřen.
Pokud byl zadán přepínač -g, dané otevření souboru bude zároveň přiřazeno do skupiny s názvem GROUP. GROUP může být název jak existující, tak nové skupiny.
mole [-m] [FILTERS] [DIRECTORY] – Pokud DIRECTORY odpovídá existujícímu adresáři, skript z daného adresáře vybere soubor, který má být otevřen.
Pokud nebyl zadán adresář, předpokládá se aktuální adresář.
Pokud bylo v daném adresáři editováno skriptem více souborů, vybere se soubor, který byl pomocí skriptu otevřen (editován) jako poslední.
Pokud byl zadán argument -m, tak skript vybere soubor, který byl pomocí skriptu otevřen (editován) nejčastěji.
Pokud bude při použití přepínače -m nalezeno více souborů se stejným maximálním počtem otevření, může mole vybrat kterýkoliv z nich.
Výběr souboru může být dále ovlivněn zadanými filtry FILTERS.
Pokud nebyl v daném adresáři otevřen (editován) ještě žádný soubor, případně žádný soubor nevyhovuje zadaným filtrům, jedná se o chybu.
mole list [FILTERS] [DIRECTORY] – Skript zobrazí seznam souborů, které byly v daném adresáři otevřeny (editovány) pomocí skriptu.
Pokud nebyl zadán adresář, předpokládá se aktuální adresář.
Seznam souborů může být filtrován pomocí FILTERS.
Seznam souborů bude lexikograficky seřazen a každý soubor bude uveden na samostatném řádku.
Každý řádek bude mít formát FILENAME:<INDENT>GROUP_1,GROUP_2,..., kde FILENAME je jméno souboru (i s jeho případnými příponami), <INDENT> je počet mezer potřebných k zarovnání a GROUP_* jsou názvy skupin, u kterých je soubor evidován.
Seznam skupin bude lexikograficky seřazen.
Pokud budou skupiny upřesněny pomocí přepínače -g (viz sekce FILTRY), uvažujte při výpisu souborů a skupin pouze záznamy patřící do těchto skupin.
Pokud soubor nepatří do žádné skupiny, bude namísto seznamu skupin vypsán pouze znak -.
Minimální počet mezer použitých k zarovnání (INDENT) je jedna. Každý řádek bude zarovnán tak, aby seznam skupin začínal na stejné pozici. Tedy např:
FILE1:  grp1,grp2
FILE10: grp1,grp3
FILE:   -
mole secret-log [-b DATE] [-a DATE] [DIRECTORY1 [DIRECTORY2 [...]]] – Skript za účelem dopadení krtka vytvoří tajný komprimovaný log s informacemi o souborech otevřených (editovaných) skrze skript mole.
Pokud byly zadány adresáře, tajný log bude obsahovat záznamy o otevřených (editovaných) souborech pouze z těchto adresářů. Neexistující adresáře nebo adresáře bez záznamů budou ignorovány.
Pokud nebyl zadán žádný adresář, tajný log bude obsahovat záznamy ze všech evidovaných adresářů.
Otevřené (editované) soubory, které mají být v tajném logu zaznamenány, je možné dále omezit pomocí filtrů -a a -b (viz níže).
