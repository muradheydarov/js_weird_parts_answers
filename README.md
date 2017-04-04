# js_weird_parts_answers

1.	Fərz edək ki, bizin bir insan obyektimiz var və biz həmən o obyektən qadın və kişi obyektləri yaratmaq istəyirik. Amma bu yeni yaratdığımız obyektlərə yenidən insan obyektinə verdiyimiz xüsusiyyətləri təkrar vermək istəmirik. Bunun üçün biz prototype məntiqindən istifadə edirik. Ümumiyyətlə javascripdə hər bir yeni yaradılan obyektin içərisində gizli prototype propertisi olur hansı ki, onnan yaradılan başqa obyektlərlə əlaqə yaradıb miras ötürə bilməsi üçün. Məsələn,
var insan = {
	head=true;
	leg=true;
	arm=true;
}
kisi.__proto__=insan;

var kisi = {
	talking=true;
	walking=true;
}

Artıq kisi obyekti öz prametrləri ilə bərabər insan obyektinin də prametrlərini daşıyır.

2.	Closure hər hansı bir funksiyanın özündən bir üst seviyyedeki funksiyaların dəyişənlərinə reach eliyə bilməsi dəməkdi. Bu bir neçə mərhələdə işləyir biz hər hansı  bir funksiya vasitəsilə bir dəyişəni tapmaq istədiyimiz zaman o birinci mərhələdə həmən dəyişəni öz lokal skopunda axtaracaq əgər tapa bilməsə özündən bir üst səviyyədəki funksiyanı araşdırcaq əgər yenə tapa bilməsə yenə bir üstə qalxacaq  ta ki, o dəyişəni tapana qədər bir üst səviyyəyə qalacaq. Əgər funksiyaların içində həmən dəyişəni tapmasa son olaraq globalı yoxlayacaq orda da tapa bilməsə undifined çıxardacaq. 

3.	x===’object’ , bu yazılış düzgün deyil çünki x – in özü heç vaxt obyektə bərabər ola bilməz amma biz onun əvəzinə x əgər obyekdirsə x.typeof yazıb yoxlaya bilərik.

4.	ECMAScript 5 satandartında əgər biz bir dəyişəni declare eləməsək o zaman console bizə error qaytaracaq çünki bu standartlar altında var-sız dəyişən təyin etmək olmaz. Bundan başqa dəyişən təyin etdiyin zaman onun qabağına var yazılanda o local olur və ancaq həmən scopda ona reach eləmək olur. Məsəl üçün,

var a = 'Rehim';   
myfunction = function(){
  var a = "Adil"
  alert("Salam, " + a ) 
}

	myfunction();  //alerts 'salam, Adil' >>> biz burda myFunctionu cagirmisiq deye funksiya ise dusen kimi birinci oz local scopundaki a ni axtarir ve a = “Adil”  oldugu ucun Adili goturur eger biz a nin qabagindan var i silsek ve yene funksiyani ise salsaq yene de netice deyismeyecek cunki funksiya yene oz local scopuna birinci baxacaq.
	alert(a); // ‘salam, Rehim’ >>> burda isə biz alert funksiyasini window da ise saliriq bu zaman funksiya birinci window ucun global deyisenleri yoxlayacaq tapa bileyenden sonra local deyisenleri yoxlayacaq yuxardaki misalda da window ucun global deyisen olmadigina gore alert Rehimi qaytaracaq. Eger biz yuxardaki misali deyisib bu cur yazsaq

var a = 'Rehim';   
myfunction = function(){
  a = "Adil"
  alert("Salam, " + a ) 
}
 
Bu zaman a = ‘Adil’ window ucun global deyisen sayildigi ucun biz alert(a) yazanda cavab Adil olacaq.

5.	== bu beraberlik datalarin deyerini yoxlayir === bu beraberlik ise hem datanin deyerini hem de tipini yoxlayir. Meselen, 
5==”5” // true qaytarir cunki her ikisinin deyeri 5di.
5===”5” // bu ise false qaytarir cunki deyerleri beraber olsa da data tipleri ferqlidi 1cisi number ikincisi ise stringdi.

6.	Number, boolean, string, null, undifined, NaN, objects, Symbol (new in ECMAScript 6)

7.	1-ci sualin cavabi 123 du cunki 1 string yazildigi ve ondan sonra number geldiyi ucun + isaresi toplama yox birlesdirme funksiyasini yerine yetirir.

8.	Iki cur yanasma var unobtrusive ve obtrusive. Bu bir novu css i html in icinde yazmaq kimi bir seydi. Eger sen js funksiyalarini HTML taginin icinde yazirsansa bu obtrusive di yox eger script tagini icinde yazirsansa bu unobtrusive di. Meselen,

Unobtrusive

<div id="informationHeader">Information</div>

<scritp>
  var a = document.getElementById("informationHeader");
  a.addEventListener("click",function(){
  alert('unobstrusive')
  })
</scritp>

Obtrusive

<div onclick="alert('obstrusive')">Information</div>

9.	Ele bil ki senin 1 ay sonra dogulacaq usagina ad qoymusan her defe onu cagirirsan. Tebii ki anadan olmayan usaq sene cavab vere bilmez. Amma bir ay sonra ne zaman ki usaq dogulacaq o artiq sene cavab verecek. Js de de eger bir deyisen teyin eleyib ona bir deyer oturmeyib onu cagirmaga calissan o sene undifined qaytaracaq ta ki sen ona bir deyer teyin edene qeder. Undifined bir error deyil sadece deyir ki bele bir adda deyisen var sadece ona deyer teyin olunmayib.  Meselen,

var a;
console.log(a) // undifined;

		Null – ise her hansi bir deyisene teyin oluna biler menasi ise hemen deyisene bir deyer teyin olunub amma ne teyin olundugu bilinmir. Meselen,

	var a = null;
	console.log(a) // null;
	typeof a = “object”

10.	 Esas conditinal statementler if else if else dir. Bunlara elave olaraq switch case ler de var. Meselen, 

if (condition_1)
   statement_1
else if (condition_2)
   statement_2
else
   statement_n;

switch (expression) {
   case label_1:
      statements_1
      [break;]
   case label_2:
      statements_2
      [break;]
   ...
   default:
     statements_n
     [break;]
}

11.	 Menasi not a number demekdir, cox nadir hallarda deyer qaytarir esasen Math funksiyalarinda. Meselen, -1 in kokunu almaga calisaq

(Math.sqrt(-1)) // NaN 
(Math.sqrt(16)) // 4

Teyin olunmus bir deyerin number olub olmadigini cox rahatliqla isNaN() funksiyasi ile yoxlaya bilerik. Meselen,

isNaN(123) //false
isNaN(-1.23) //false
isNaN(5-2) //false
isNaN(0) //false
isNaN('123') //false
isNaN('Hello') //true
isNaN('') //false
isNaN(true) //false
isNaN(undefined) //true
isNaN('NaN') //true
isNaN(NaN) //true
isNaN(0 / 0) //true

12.	This shexs evezliklerine cox oxsayir meselen, Rehim Qubaya getdi. O, 2 gun sonra Bakiya qayitdi. Biz bu cumleni bele de yaza bilerik, Rehim 2 gun sonra Bakiya qayitdi. Eyni adi tekrar istifade etmemek ucun O evezliyinden istifade olunur hansi ki deyeri Rehime beraberdir. Js de ise bu sexs evezliyini this evez edir. Meselen, 
		<div id="myDiv" style="width:100px;height:100px;background:red;"></div>
		var a = document.getElementById('myDiv');
    		a.addEventListener("click",function() {
      	this.style.display="none"; // this-in evezine men a da yazsam eyni netice olacaq
    		})
	This-in en onemli xususiyyetlerinden biri de this funksiya ise dusmeyene qeder teyin olunmur. Meselen,
		<div id="myDiv" style="width:100px;height:100px;background:red;"></div>
		var a = document.getElementById('myDiv');
		console.log(this) // 1
    		a.addEventListener("click",function() {
      	this.style.display="none"; // this-in evezine men a da yazsam eyni netice olacaq
		console.log(this) // 2
    		})
	Bu iki this bir birinden ferqlidir. 1-ci this-I console.log elesek o bize window qaytaracaq cunki o hec bir funksiyanin icinde deyil. Amma ikinci this bize hec ne qaytarmayacaq ta ki biz dive click edene qeder. Biz dive click edenden sonra o bize hemen divi qaytaracaq. Bu misaldan da anlasildigi kimi this ancaq funksiya ise dusen zaman teyin olunur.

13.	 Aralarindaki en boyuk ferq not defined errordu undefined ise data tipidi. Meselen,
var a;
console.log(a) // undefined;
console.log(b) // error b is not defined;

14.	 Hoisting javascripting default funksiyasidi. Script ise dusen ki funksiyalar ve windowda var ile teyin olunan deyisenler scriptin en basina qalxir. Bu o demekdir ki, biz hemen funksiyalari scrpitin istenilen yerinde cagira bilerik ve ya hemen deyisenleri istediyimiz yerde istifade ede bilerik. Deyisenlerle bagli her hansi bir problemin olmamasi ucun global deyisenleri scriptin en basinda yazmaq meslehetdir ki sonra hemen deyiseni funksiya ve ya obyektde istifade etdiyimiz zaman undefined problem yasamayaq. Meselen,

var name = "Adil";

(function() {
  console.log("My name is " + name); // My name is Adil
})()

(function() {
  console.log("My name is " + name); // My name is Adil;
})()

var name = "Adil";

her iki misal eyni neticeni verir amma var funksiyanin icinde yazildigi zaman veziyyet ferqlidir.

(function() {
	 var name = "Adil";
  console.log("My name is " + name); // My name is Adil
})()

(function() {
console.log("My name is " + name); // My name is undefined;
var name = "Adil";

})()

	Birinci funksiyada deyisen console funksiyasindan yuxarinda yerlesdiyi ucun eyni netice alinir. Amma ikinci funksiyada deyisen console funksiyasindan asagida yerlesdiyi ucun deyisenin deyeri undefined olur.

15.	 OOP (prototype-based) ve Funksional paradigmalar extra (imperativ);

16.	 Qarşında duran problemə funksiyalarla müdaxilə etməyini istəyir. Əsas məntiq hər bir şeyi funksiya ilə yaz lazım olduqca təzdən çağır. Funksional paradigmanin da musbet ve menfi cehetleri var en boyuk menfi ceheti miras oture bilmemesi, musbet ceheti ise kod tekrarini azaldir ve bir funksiyada olan error butun funksiyani saxlamir.

17.	Classic inheritance ile prototypal inheritance kernardan bir birine benzeselerde eslinde ferqli seylerdi. Tesevvur edek ki bizim bir person obyektimiz var ve biz bu obyekten miras alan yeni obyektler yaratmaq isteyirik əgər biz classic inheritance vasitesile yeni bir obyekt yaratmaq isteyirikse o zaman yeni yaratdigimiz obyekt ozune lazim olan olmayan butun parametrleri, motodlari oz parentinden miras alib saxlayacaq. Təbii ki bu da yaddasda lazimsiz elave yer tutacaq. Amma prototypal inheritance ise Js i belke de bu qeder mehsur eden xususiyyetlerden biridir. Bele ki, prototypal inheritance eyni metod ve propertileri oz parentinden miras alir lakin parametrlere yeni deyer oturmediyi muddetce hemen parametrler yaddasda yer turmur. 
	Yekun olaraq classic inheritace ile yeni obyekt yaratdigimiz zaman o miras alidigi butun property ve metodlari yeniden yaddasa yazir amma prototypal inheritance de ise sadece deyisen property ve metodlar yaddasa yazilir. 
18.	 Functional programming:
Pros: sistemli yazilis, kod tekrarinin azligi, debag elemek cox rahat olur
Cons: miras oturmek mumkun deyil.

OOP:
Pros: class mentinqinin olmasi (js de prototype), az yaddasla cox data ile islemek qabiliyyeti, komanda seklinde islemek ucun ela serait yaradir.
Cons: Bezen cox qarisiq hala gele bilmesi, debagging in cetin olmasi.

19.	 Əgər bir constructor functiondan bir obyekt yaradacaqsansa ve onun bütün medot ve propertilerinden istidade edeceksense onda istifade etmek olar amma yene de js prototypal inheritance meslehet olardi.

20.	  Ümumiyyetle götürəndə həmişə istifadə olunması məsləhətdi amma daha çox bir nece sayda obyekt yaradan zaman istifadə olunur.

21.	???

22.	???

23.	???

24.	
