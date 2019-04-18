# AngularJS
Crie webapps poderosas

* Instalar Node.js: https://nodejs.org/

**comandos Node.js**
npm install (baixar módulos no projeto)
npm start (inicia o servidor - url: localhost:3000 - default)

**tags AngularJS**
**Diretivas**
ng-app (inicializa o módulo principal)
ng-controller (inicializa o controller usado)

data-bind = dados dinamicos atrelados entre view e controller
angular expressions: {{}} (lacunas nas paginas onde entra o código do angular)
view: nome dado as htmls
separar controllers em arquivos distintos
arquivos js: em letras minúsculas separados por hífen (EX: fotos-controller.js)
modulos angular: com iniciais das palavras com letras maiúsculas (EX: FotosController)


projeto Angular.js
----
**Aula 1**
importar scripts do angular: <script src="js/lib/angular.min.js"></script>
criar um modulo principal: main.js
criar o módulo principal: angular.module('alurapic', []);
importar o js do módulo no html principal: <script src="js/main.js"></script>
inicializar o módulo criado no html principal: <html lang="pt-br" ng-app="alurapic">
criar módulos secundários separados: angular.module('alurapic').controller('FotosController', function($scope)) {
inicializar o módulo secundário no html principal: <body ng-controller="FotosController">

**Aula 2**
ng-repeat para vários $scope
padrão promisse para o $http
 *...
	$scope.fotos = [];
	$http.get('v1/fotos')
	.success(function(fotos){
		$scope.fotos = fotos;
	})
	.error(function(erro) {
		console.log(erro);
	})
 ...*
 
**Aula 3 - Criando Diretivas**

criar a diretiva em js separado:
	angular.module('minhasDiretivas', []).directive('meuPainel', function() {}
criar variável ddo e configurar os atributos:
	- restrict: "AE";
	- transclude;
	- scope (com os atributos que passarão da html pro painel da diretiva)
	- template (com a html inclusa)
	- templateUrl (com o caminho da Url utilizada pela diretiva)
	
importar o js da diretiva na página principal: <script src="js/directives/minhas-diretivas.js"></script>

**Aula 4 - Melhorando a experiência do usuário**
	a diretiva ng-model e two-way data binding
	aplicação de filtro na diretiva ng-repeat
	ng-model-options e postergação do two-way data binding
	animações com o módulo ngAnimate
	animações requerem conhecimento sólido de CSS3
filtro no angular usa-se o | (pipe) (EX: ng-repeat="funcionario in funcionarios | filter: {nome: textoFiltro} ")
ng-repeat aceita filter
ngAnimate é a diretive que adicionada ativa as animações

**Aula 5 - Dividir para conquistar!**
dividir a aplicação em várias páginas (single page application)
incluir lacuna <ng-view> no index que carregará as páginas
importar js de rotas 
	<script src="js/lib/angular-route.min.js"></script>

configurar rotas no módulo principal
	angular.module('alurapic', ['minhasDiretivas', 'ngAnimate', 'ngRoute'])
	.config(function($routeProvider){

		$routeProvider.when('/fotos', {
			templateUrl: 'partials/principal.html',
			controller: 'FotosController'
		});
	});
	
adicionar rota default para qq rota que não esteja mapeada:
		$routeProvider.otherwise({ redirectTo: '/fotos'});