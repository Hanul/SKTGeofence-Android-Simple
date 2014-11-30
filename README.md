# SKT Geofence API Android Simple Library
SKT Geofence API를 쉽게 사용할 수 있도록 Wrapping한 Library 입니다.
* [Tdev-Geo-fence-android_sdk.jar](https://developers.sktelecom.com/content/tapi/Geo-fence/)가 필요합니다.
* [UPPERCASE.JAVA-JSON-UTIL.jar](https://github.com/Hanul/UPPERCASE.JAVA-JSON-UTIL)가 필요합니다.
* 기기에 SKT Geofence Agent가 설치되어 있어야 합니다.

## 설치
1. 프로젝트의 `lib` 폴더에 `bin/sktgeofence-android-simple.jar` 파일을 복사합니다.
2. 프로젝트의 `AndroidManifest.xml`에 인터넷 Permission을 작성합니다.
```XML
<uses-permission android:name="android.permission.INTERNET" />
```
3. 프로젝트의 `AndroidManifest.xml` 내용 중 `application` 이하에 하단의 내용을 추가합니다. `{{YOUR PACKAGE NAME}}` 부분에는 프로젝트의 패키지 명을 입력합니다.
```XML
<receiver android:enabled="true" android:exported="true" android:name="com.btncafe.cordova.sktgeofence.SKTGeofenceServiceReceiver">
	<intent-filter>
    	<action android:name="{{YOUR PACKAGE NAME}}.GEOEVENT" />
    </intent-filter>
</receiver>
```

## API
#### 초기화
* `new SKTGeofence(Context context, String packageName, String tdcProjectKey, ConnectedListener connectedListener)` Geofence API를 초기화하고, SKT GeoFenceAgent와 연결합니다. 연결이 되면, connectedListener을 실행합니다.
* `sktgeofence.setCheckInHandler(CheckInHandler checkInHandler)` 특정 펜스 내에 Check In 하였을때 실행할 Handler를 등록합니다. Handler는 Store Id를 가져옵니다.

해당 플러그인은 Store Group, Store, Event Group, Event 네가지 데이터의 처리를 제공합니다.
#### Store Group
* `sktgeofence.createStoreGroup(JSONObject data, Handler handler)` 매장 그룹 정보를 생성하고, 정보를 가져옵니다.
* `sktgeofence.getStoreGroup(int storeGroupId, Handler handler)` storeGroupId에 해당하는 매장 그룹 정보를 가져옵니다.
* `sktgeofence.updateStoreGroup(JSONObject data, Handler handler)` data의 storeGroupId에 해당하는 매장 그룹 정보를 수정하고, 수정된 정보를 가져옵니다.
* `sktgeofence.removeStoreGroup(int storeGroupId)` storeGroupId에 해당하는 매장 그룹 정보를 삭제합니다.
* `sktgeofence.getAllStoreGroupList(ListHandler listHandler)` 모든 매장 그룹 정보를 가져옵니다.

###### Store Group Data 형태
| Name      | Type   | Description |
|-----------|--------|-------------|
| groupName | String | 매장 그룹명   |

#### Store
* `sktgeofence.createStore(JSONObject data, Handler handler)` 매장 정보를 생성하고, 정보를 가져옵니다.
* `sktgeofence.getStore(int storeId, Handler handler)` storeId에 해당하는 매장 정보를 가져옵니다.
* `sktgeofence.updateStore(JSONObject data, Handler handler)` data의 storeId에 해당하는 매장 정보를 수정하고, 수정된 정보를 가져옵니다.
* `sktgeofence.removeStore(int storeId)` storeId에 해당하는 매장 정보를 삭제합니다.
* `sktgeofence.getStoreListInGroup(int storeGroupId, ListHandler listHandler)` storeGroupId에 해당하는 매장 그룹 내의 모든 매장 정보를 가져옵니다.

###### Strore Data 형태
| Name         | Type    | Description  |
|--------------|---------|--------------|
| storeGroupId | Integer | 매장 그룹 ID  |
| name         | String  | 매장명        |
| latitude     | Double  | 매장 위치 위도 |
| longitude    | Double  | 매장 위치 경도 |

#### Event Group
* `sktgeofence.createEventGroup(JSONObject data, Handler handler)` 이벤트 그룹 정보를 생성하고, 정보를 가져옵니다.
* `sktgeofence.getEventGroup(int eventGroupId, Handler handler)` eventGroupId에 해당하는 이벤트 그룹 정보를 가져옵니다.
* `sktgeofence.updateEventGroup(JSONObject data, Handler handler)` data의 eventGroupId에 해당하는 이벤트 그룹 정보를 수정하고, 수정된 정보를 가져옵니다.
* `sktgeofence.removeEventGroup(int eventGroupId)` eventGroupId에 해당하는 이벤트 그룹 정보를 삭제합니다.
* `sktgeofence.getAllEventGroupList(ListHandler listHandler)` 모든 이벤트 그룹 정보를 가져옵니다.

###### Event Group Data 형태
| Name      | Type   | Description |
|-----------|--------|-------------|
| groupName | String | 이벤트 그룹명   |
| startDate | String | 이벤트 시작 일자 (예: 2014-11-21)   |
| endDate   | String | 이벤트 종료 일자 (예: 2014-11-30) |

#### Event
* `sktgeofence.createEvent(JSONObject data, Handler handler)` 이벤트 정보를 생성하고, 정보를 가져옵니다.
* `sktgeofence.getEvent(int eventId, Handler handler)` eventId에 해당하는 이벤트 정보를 가져옵니다. (현재 Geofence API 에서는 작동하지 않습니다. 추후 업데이트 예정)
* `sktgeofence.updateEvent(JSONObject data, Handler handler)` eventId에 해당하는 이벤트 정보를 수정하고, 수정된 정보를 가져옵니다. (현재 Geofence API 에서는 작동하지 않습니다. 추후 업데이트 예정)
* `sktgeofence.removeEvent(int eventId)` eventId에 해당하는 이벤트 정보를 삭제합니다.
* `sktgeofence.getEventListByStore(int storeId, ListHandler listHandler)` 특정 매장이 속해있는 모든 이벤트 정보를 가져옵니다.

###### Event Data 형태
| Name           | Type    | Description  |
|----------------|---------|--------------|
| eventGroupId   | Integer | 이벤트 그룹 ID  |
| name           | String  | 이벤트 명        |
| eventCheckType | String  | 이벤트 체크 방법 (CheckIn : 팬스 안으로 진입 시, CheckOut : 팬스 밖으로 나갈 때, Stay : 팬스 안에서 머무를 때) |
| storeId        | Integer | 매장 ID        |

## License
[MIT](LICENSE)
* Geofence API와 관련된 License는 [SK Telecom](http://www.sktelecom.com)에 있습니다.

## 작성자
[심영재](https://github.com/Hanul)
