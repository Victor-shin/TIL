## LOGIN 화면을 위한 화면 구성을 별도로 하고 싶다.
##### STEP1: index.html에서 head와 body를 분리한다.
```
		<div ui-view="head"></div>
		<div class="container">
			<div class="row">
				<div class="col-md-10 col-md-offset-1">
					<div ui-view="body"></div>
				</div>
			</div>
		</div>
```
##### STEP2: client설정 스크립트에서 state별로 views 옵션으로 각각 설정한다.
```
            .state('history', {
                url: '/history',
                data: {
                    requireLogin: true
                },
                views: {
                    "head": {
                        templateUrl: '/html/navigation.html',
                        controller: 'NavCtrl'
                    },
                    "body": {
                        templateUrl: '/html/history.html',
                        controller: 'HistoryCtrl'
                    }
                },                
                resolve: {
                    jobPromise: ['jobs', function(jobs){
                        return jobs.getJobHistory("__ALL__", 1);
                    }]
                }
            })
            .state('login', {
                url: '/login',
                onEnter: ['$state', 'auth', function($state, auth){
                    if(auth.isLoggedIn()){
                        $state.go('main');
                    }
                }],
                data: {
                    requireLogin: false
                },
                views: {
                    "body": {
                        templateUrl: '/html/login.html',
                        controller: 'AuthCtrl'
                    }
                }
            });
```
