# FAB
플로팅 액션버튼 사용을 위한 예시 저장소


#### 플로팅 버튼 라이브러리 
	
	compile 'com.github.clans:fab:1.6.4'

	이거 깔고 해줘야될게 많은데 일단 res폴더에 anim 이랑 ,drawable 폴더를 만들어야 하고 몇가지 파일들을 집어넣어야 한다.
	values - styles.xml 에 몇가지를 추가하여야 한다.  

	*** 특이사항  :  menu 버튼의 경우 클릭리스너를 달아주지 않아도 animation작동을 한다. 애초에 그렇게 구성된 라이브러리인것 같다. 


#### :x:  xml 사용 예시 :
```java

		// FAB 메뉴 이며 클릭시 FAB 3개가 나오는 예제이다.
		// 상단 레이아웃에 xmlns:fab="http://schemas.android.com/apk/res-auto"  를 추가해줘야한다.

        <com.github.clans.fab.FloatingActionMenu
        android:id="@+id/fabMenu"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        fab:menu_labels_style="@style/MenuButtonsSmall.Blue" // 스타일에 추가해야 한다. 새로운 이름을 짓거나 색깔 조절 가능하다.
        fab:menu_labels_showAnimation="@anim/jump_from_down" // anim 폴더에 추가해야 하는 부분 
        fab:menu_labels_hideAnimation="@anim/jump_to_down"	 // anim 폴더에 추가해야 하는 부분
        fab:menu_animationDelayPerItem="0"
        fab:menu_shadowColor="#444"
        fab:menu_colorNormal="#35cdd5"
        fab:menu_colorPressed="#2fb8c0"
        fab:menu_colorRipple="#259197"
        android:layout_above="@+id/tab"
        android:layout_alignParentRight="true"
        android:layout_alignParentEnd="true">

        <com.github.clans.fab.FloatingActionButton
            android:id="@+id/fabAcc"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:src="@drawable/ic_aa"
            fab:fab_label="계좌 메모"						// FAB 메뉴를 눌러 버튼이 펼쳐졌을때 펼쳐진 버튼 옆에 붙는 설명 
            style="@style/MenuButtonsSmall.Blue" />

        <com.github.clans.fab.FloatingActionButton
            android:id="@+id/fabId"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:src="@drawable/ic_aa"
            fab:fab_label="아이디 메모"						// FAB 메뉴를 눌러 버튼이 펼쳐졌을때 펼쳐진 버튼 옆에 붙는 설명 
            style="@style/MenuButtonsSmall.Blue" />

        <com.github.clans.fab.FloatingActionButton
            android:id="@+id/fabText"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:src="@drawable/ic_aa"
            fab:fab_label="메모 추가"						// FAB 메뉴를 눌러 버튼이 펼쳐졌을때 펼쳐진 버튼 옆에 붙는 설명 
            style="@style/MenuButtonsSmall.Blue" />
    </com.github.clans.fab.FloatingActionMenu>
```

#### :x:  액티비티 내부 사용 예시 :
 ```
 	// 선언부 
 	private FloatingActionButton fabText;
    private FloatingActionButton fabId;
    private FloatingActionButton fabAcc;
    private FloatingActionMenu  fabMenu;

    //onCreate 내부 
    fabText = (FloatingActionButton) findViewById(R.id.fabText);
    fabId = (FloatingActionButton) findViewById(R.id.fabId);
    fabAcc = (FloatingActionButton) findViewById(R.id.fabAcc);
    fabMenu = (FloatingActionMenu) findViewById(R.id.fabMenu);

    // onclick 세팅 
    fabId.setOnClickListener(clickListener);
    fabText.setOnClickListener(clickListener);
    fabAcc.setOnClickListener(clickListener);

    // 기타 특이사항 
    // FAB를 통해 다른 Activity나 fragment 로 이동하였다면 fabMenu.close(true); 를 통해 닫아줘야한다.  안그러면 돌아왔을때 열려있음.


```



* 액티비티에서 플로팅 버튼(Floating action button) 사용할 때 editText 에서 자동으로 플로팅 버튼 올라오게 / 안 올라오게 하는 것 
 : 	manifest 에서 각 activity에 설정 해줘야 하는데 
 1. 프래그먼트는 아래 기본 설정이 adjustResize 이다. 프래그먼트에 FAB를 띄울때는 자동으로 올라온다고 한다.
 2. 액티비티는 아래 기본 설정이 adjustNoting 이다. 액티비티에 FAB를 띄우면 자동으로 안올라온다.
 	android:windowSoftInputMode="adjustNothing" 라고 하면 안올라온다.
 	android:windowSoftInputMode="adjustResize" 라고 하면 키보드가 올라올 때 activity 크기가 리사이즈 된다. 