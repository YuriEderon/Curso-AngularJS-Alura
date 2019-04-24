ng-app - define o módulo de aplicação
EX: <html ng-app"store">

ng-controller - define uma função de controle
EX: <body ng-controller="StoreController as store">

ng-show / ng-hide - Exibe um valor de acordo com um expressão
EX: <h1 ng-show="name"> Hello, {{name}}! </h1>

ng-repeat
EX: <li ng-repeat="product in store.products"> {{products.name}} </li>

ng-click = ativa uma função
ng-model

{{data|filter:options}} - filtros
EX: date - {{'1388123412323 | date:'MM/dd/yyyy @ h:mma'}} = 12/27/2013 @ 12:50AM
	uppercase & lowercase - {{'octagon gem' | uppercase}} = OCTAGON GEM
	limitTo - {{'My Description' | limitTo:8}} = My Descr
	orderBy - <li ng-repeat="product in store.products | orderBy:'-price'"> "descending price"
			  <li ng-repeat="product in store.products | orderBy:'price'"> "ascending price"
			  
ng-src - caminho de imagens
EX: <img ng-src="{{product.images[0]}}">

ng-init - inicializa algo
EX: <section ng-init="tab = 1">

ng-class - ativa uma class dependendo da condição
EX: <li ng-class="{ active: tab === 1}"> *active é o nome da class da folha de estilo.

ng-submit - indica no form qual função do controle é utilizada após um submit

ng-include - insere um html dentro de outro
EX: <h3 ng-include="'produto_campo.html'"></h3> <--- ' para variáveis

Controle
EX:
app.controller('GalleryController', function(){
  this.current = 0;
  this.setCurrent = function(newGallery){
    this.current = newGallery || 0;
  };
});
  
EX:
app.controller('ReviewController', function(){
  this.review = [];
  this.addReview = function(product){
    product.reviews.push(this.review);
    this.review = [];
  };
});

 Validacao
 novalidate - usada na tag "form", retira as validação padrões dos browsers
 required - usada nos campos para forçar uma validação a um campo
 $valid - usada para saber se as variáveis ""/o controlle	

.ng-invalid.ng-dirty {
  border-color: red;
}
  
.ng-valid.ng-dirty {
  border-color: green;
}

Diretivas - criação de tags customizadas
EX:

** index.html **
<product-title></product-title> - Element
<h3 product-title></h3> Attribute

OBS: evitar <product-title/>

** app.js **
app.directive('productTitle', function(){
	return {
		restrict: 'E',  <--- (E for Element / A for Attribute)
		templateUrl: 'product-title.html', <--- Url do template
		
		---caso tenha controler---
		controller: function(){
		...
		}
		controllerAs: 'panels'
	};
});

** product-title.html **
<h3>
	{{product.name}}
	<em class="pull-right">$250.00</em>
</h3>

Modulos - js combinados
var app = angular.module('store', ['store-products']); (js primário)
var app = angular.module('store-products',[]); (modulo js)

OBS: incluir js dependente na inclusão dos outros js.

Services
$http, $log, $filter etc...
EX:
$http({ method: 'GET', url: '/products.json' }); (.success() ou .error())
$http.get('/products.json', { apiKey: 'myApiKey' }); (.success() ou .error())

Dependency injection
app.controller('SomeController', ['$http', function($http){
}]); (1 serviço)
app.controller('SomeController', ['$http', '$log', function($http, $log){
}]); (Mais de 1 serviço)

EX:
var app = angular.module('store', ['store-products']);

app.controller('StoreController', ['$http', function($http){
	var store = this;
	store.products = [];
	$http.get('/products.json').success(functions(data){
		store.products = data;
	});
}]);

$http.post('/path/to/resource.json',{ param: 'value' });
$http.delete('/path/to/resource.json');
$http({ method: 'OPTIONS', url: '/path/to/resource.json' });
$http({ method: 'PATCH', url: '/path/to/resource.json' });
$http({ method: 'TRACE', url: '/path/to/resource.json' });
