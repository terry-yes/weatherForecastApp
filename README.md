



#### π± μ΄ νλ‘μ νΈλ kxcoding.comμ Step By Step Weather App κ°μλ₯Ό ν΅ν΄ λ§λ  `λ μ¨ App`μλλ€.

# λ μ¨ μ±

![forecast view low-min](https://user-images.githubusercontent.com/55867479/118953266-9ff89200-b997-11eb-9e91-754c3feef768.gif)

## 1. νλ©΄ κ΅¬μ±

<img width="200" alt="Screen Shot 2021-05-19 at 12 04 15 AM" src="https://user-images.githubusercontent.com/55867479/118953296-a71fa000-b997-11eb-84fa-8e573ce9427d.png">

- νλ©΄μ νλμ νμ΄λΈ λ·°κ° 2κ°μ μΉμμΌλ‘ λλμ΄μ Έ μμ΅λλ€.
- μ²«λ²μ§Έ μΉμμλ νμ¬ λ μ¨λ₯Ό νμνλ μμ΄ 1κ° νμλ©λλ€.
- λλ²μ§Έ μΉμμλ λ μ¨ μλ³΄λ₯Ό νμνλ μμ΄ APIμλ²μμ κ°μ Έμ¨ κ°―μλ§νΌ νμλ©λλ€.

<img width="200" alt="λ©μΈνλ©΄ μ€ν¬λ‘€μ  2" src="https://user-images.githubusercontent.com/55867479/118953300-a7b83680-b997-11eb-8a02-1e402b86e5da.png">


- μ€μ λ‘ μ±μ κ΅¬λνλ©΄ κ°μ΄λ° μ¬λ°±μ΄ μλλ° μ΄λΆλΆμ νμ΄λΈλ·°μ contenInsetμΌλ‘ 1λ²μ§Έ μΉμμ λμ΄λ₯Ό λμ μΌλ‘ κ³μ°νμ¬ λ§¨λ°μ λ°°μΉλλλ‘ ν©λλ€.
- μμ 3κ°μ λΉ¨κ°μ μ¬κ°νμ€ κ°μ΄λ°κ° InsetλΆλΆμλλ€. μ²«λ²μ§Έ μΉμμ μμμ΄ 3λ²μ§Έ μ¬κ°νλΆλΆ μλλ€.


## 2. νλ‘μ νΈ κ΅¬μ‘°

### π ν΄λ κ΅¬μ‘°
```
Forecast/
ββ Location/
β  ββ LocationManager.swift
ββ Formatter/
β  ββ Double+Formatter.swift
β  ββ Date+Formatter.swift
ββ Data/
β  ββ WeatherDataSource.swift
ββ Model/
β  ββ ApiError.swift
β  ββ CurrentWeather.swift
β  ββ Forecast.swift
ββ Cell/
β  ββ SummaryTableViewCell.swift
β  ββ ForecastTableViewCell.swift
AppDelegate.swift
SceneDelegate.swift
Common.swift
ViewController.swift
Main.storyboard
LaunchScreen.storyboard
Info.plist
```

#### π LocationManager
- μμΉμ κ΄λ ¨λ κΆνμ νμΈνκ³  μ¬μ©μμκ² μμ²­ν©λλ€. (CLLocationManager, CLAuthorizationStatus)
  - iOS 14.0 μ΄μμμλ CLLocationManagerμ μΈμ€ν΄μ€ λ©μλμΈ authorizatinoStatusλ‘ μ΄κΈ°νν©λλ€.
  - κ·Έ μ΄νλ²μ μμλ CLLocationManager.authorizationStatus() νμ λ©μλλ‘ μ΄κΈ°νν©λλ€.
- κΆνμ νμΈμ CLLocationManagerDelegateλ₯Ό μ±μ©ν΄μ νμΈν©λλ€.
  - requestWhenInUseAuthorization()μΌλ‘ κΆνμ μμ²­ν©λλ€. 
  - requestLocation()μΌλ‘ μμΉλ₯Ό μμ²­ν©λλ€. 
- μμΉλ₯Ό μμ²­νλ μ½λλ₯Ό κΆνμ μμ²­ν λ€ νΈμΆν΄μΌ ν©λλ€.
- μμ²­ν μμΉλ 2κ°μ§ ννλ‘ μ¬μ©λ©λλ€.
  - μ²«μ§Έ) μμΉλ₯Ό reverseGeocoderλ₯Ό μ¬μ©ν΄ `00κ΅¬ 00λ` νμμ μ£Όμλ‘ λ³ννμ¬ λ©μΈνλ©΄μλ¨μ νμν©λλ€.
  - λμ§Έ) μμΉλ₯Ό ν΅ν΄ OpenWeatherMap.org APIμλ²(μ΄ν APIμλ²)λ‘ μμ²­μ λ³΄λ΄ λ μ¨ μ λ³΄λ₯Ό λ°μμ΅λλ€.
- μΈλΆμμ μ¬μ©λ  λ³μ λͺ©λ‘
  - `currentLocationTitle: String?`: ooκ΅¬ ooλ νμμ μ£Όμνμ μ΄ λ³μμ property observerλ₯Ό λ¬μμ μ£Όμκ° λ°λμλ€λ μ¬μ€μ NotificationCenterμ μ λ¬ν©λλ€. μ μ²΄μ μΈ NotificationCenterμ κ΅¬μ‘°λ λ°μμ λ€μ μ€λͺνκ² μ΅λλ€.
  - `currentLocation: CLAuthorizationStatus` : APIμλ²μ μμ²­ν  μ£Όμ λ°μ΄ν°, μ¬κΈ°μμ κ°μ§λ λ³νλ λ³λμ NotificationμΌλ‘ μ²λ¦¬νμ§ μκ³  μμ `currentLocationTitle`μμ κ°μ΄ μ²λ¦¬ν΄μ€λλ€.

#### π Formatter

##### Double+Formatter.swift

- μ¨λ νμ νμμ μ€μ ν©λλ€.
- `MeasurementFormatter()`λ₯Ό ν΅ν΄ μμμ  ν΅μΌκ³Ό `Β°(λ, degree)` λ₯Ό νμν©λλ€.

##### Date+Formatter.swift

- μλ³΄μ νμν λ μ§μ μκ° νμμ μ€μ ν©λλ€.
- `DateFormtter()`λ₯Ό ν΅ν΄ μκ° νμμ μλμ κ°μ΄ ν΅μΌνμμ΅λλ€.
λ μ§: `Mμ dμΌ`νμ
μκ°: `HH:00`νμ

#### π Model

#### CurrrentWeather.swift
CurrentWeather
- APIμλ²λ‘λΆν° λ°μ "νμ¬λ μ¨" λ°μ΄ν°μ JSONνμΌμ λ΄μ νμμ μ€μ ν©λλ€.

#### Forecast.swift
Forecast
- APIμλ²λ‘λΆν° λ°μ "λ μ¨μλ³΄" λ°μ΄ν°μ JSONνμΌμ λ΄μ νμμ μ€μ ν©λλ€.

ForecastData
- κ΅¬μ‘°μ²΄κ° μ€μ²©λ νμμ λ°μ΄ν°μΈ Forecast νμμ κ°κ²°νκ² λ§λ  νμμλλ€.

#### ApiError.swift
- APIμλ²λ‘ μμ²­μ λ³΄λμλ λ°μν  μ μλ Error μ΄κ±°νμλλ€.


### π Data/WeatherDataSource.swift

- κΈ°λ₯1) LocationMangerμμ μμλΈ μμΉλ₯Ό observerλ₯Ό ν΅ν΄ κ°μ§ν©λλ€.
- κΈ°λ₯2) κ°μ§λ μμΉ μ£Όμλ₯Ό Notificationμ λ΄μ ViewControllerλ‘ λ³΄λλλ€.
- κΈ°λ₯3) κ°μ§λ μμΉ μ λ³΄λ‘ APIμλ²λ‘ λ μ¨μ λ³΄λ₯Ό μμ²­ν©λλ€.
  - λ μ¨ μ λ³΄λ 
  fetchCurrentWeather(location: , completion:), fetchForecast(location: ,completion) λ‘ νμ¬λ μ¨μ μλ³΄λ μ¨λ₯Ό λ°λ‘ μμ²­ν©λλ€.
  - λλ€ fetch(urlStr: , completion)μ νΈμΆνλλ° μ¬κΈ°μ Resultνμμ ν΅ν΄ μ±κ³΅λ λ°μ΄ν°μ μ€ν¨μ Errorμ λ΄μ λ¦¬ν΄ν©λλ€.
  - fetch(location: , completion) ν¨μλ₯Ό λ€μ λ§λ€μ΄ λ΄λΆμμ fetch(urlStr: , completion)μ μ±κ³΅ λ°μ΄ν°μ μλ¬λ₯Ό μ²λ¦¬νκ³  NotificationCenterμ μλ €μ€λλ€.


## 3. Notification Centerλ₯Ό ν΅ν λ°μ΄ν° μ λ¬

μ΄ νλ‘μ νΈμμλ μλ 2κ°μ Notificationμ΄ μμ΅λλ€.

1 currentLocationDidUpdate
  - νμ¬ μμΉλ₯Ό λλ°μ΄μ€λ‘λΆν° λ°μΌλ©΄ currentLocationTitle νλ‘νΌν°κ° μλ°μ΄νΈ λκ³  property observerλ₯Ό ν΅ν΄ Notificationμ΄ post λ©λλ€.
  - μμ Notificationμ WeatherDataSource ν΄λμ€μ μμ±μμ Observerκ° κ°μνκ³  μμ΅λλ€.
  - Observerκ° Notificationμ κ°μ§νλ©΄ 2κ°μ§ μΌμ ν©λλ€.
    1) APIμλ²λ‘ μμμ λ°μ μμΉμ λ³΄μ λν λ μ¨ μ λ³΄λ₯Ό νΈμΆν©λλ€.
    2) μλ Notificationμ postν©λλ€.

2 weatherInfoDidUpdate
  - 1μ Notificationμ observerκ° κ°μ§νλ©΄ 2λ²μ§Έ Notificationμ΄ postλ©λλ€.
  - μ΄ Notificationμ Observerλ ViewContorller.swiftμ viewDidLoadμ κ΅¬νλμ΄ μμ΅λλ€.
  - μ¬κΈ°μμ Observerκ° Notificationμ κ°μ§νλ©΄ alphaκ°μ΄ 0μ΄μλ νμ΄λΈλ·°μ alphaκ°μ΄ 1μ΄ λκ³  Acitivity Indicatorκ° μ¬λΌμ§λλ€.