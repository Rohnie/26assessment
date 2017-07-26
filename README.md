# 26assessment
HTML

<html>

<head>
  <title>Generate Menu Items</title>
  <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
  <script type="text/javascript" src="script.js"></script>
  
</head>

<body ng-app="generateApp" ng-controller="generateController">
  <form>
    <textarea ng-model="names"></textarea>
    &nbsp;
    <textarea ng-model="dates"></textarea><br>
    <input type="submit" ng-click="generateList()" />
  </form>
  <ol ng-repeat="nameDate in nameDates">
    <li>Breakfast for {{nameDate.name}} on {{nameDate.date | date: 'yyyy-MM-dd'}}</li>
    <li>Lunch for {{nameDate.name}} on {{nameDate.date | date: 'yyyy-MM-dd'}}</li>
    <li>Dinner for {{nameDate.name}} on {{nameDate.date | date: 'yyyy-MM-dd'}}</li>
  </ol>
</body>

</html>

JS

var generateApp = angular.module("generateApp", []);
generateApp.controller("generateController", function($scope) {
  $scope.generateList = function() {
    $scope.nameDates = [];

   /* console.log($scope.names + " " + $scope.dates);*/

    $scope.dateArray = $scope.dates.split("\n");
  /*  console.log($scope.dateArray);*/

    $scope.nameArray = $scope.names.split("\n");
  /*  console.log($scope.nameArray);*/

    angular.forEach($scope.dateArray, function(value, key) {
      var array = value.split(" ");
    /*  console.log(array);*/

      var fromDate = new Date(array[0]);
      var toDate = new Date(array[2]);
      var noOfDays = Math.round(
        Math.abs(fromDate.getTime() - toDate.getTime()) / (24 * 60 * 60 * 1000)
      );

     console.log(fromDate + " " + toDate + " " + noOfDays);

      if (noOfDays == 0) {
        $scope.nameDates.push({ name: $scope.nameArray[key], date: fromDate });
        
      } else {
        
        var i = 0;
        while (i <= noOfDays) {
          
          if(i == 0){
             $scope.nameDates.push({ name: $scope.nameArray[key], date: fromDate });
            
             }
          else{
            fromDate = new Date(fromDate.setDate(fromDate.getDate() + 1));
           /* console.log(fromDate)*/
          $scope.nameDates.push({
            name: $scope.nameArray[key],
            date: fromDate
          });
          }
         /* console.log(fromDate.getDate());*/
          ++i;
        }
        console.log($scope.nameDates);
      }
    });
  };
});
