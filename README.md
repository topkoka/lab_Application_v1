# 1.MVC
## 1.binding

* 1.1 เรียกใช้  binding

- app/gradle
```
 dataBinding{enabled true}
```

## 2.mvc

* 2.1 สร้าง package รูปแบบ MVC

```
-activity -manager -util -view -fragment
```

* 2.2 สร้าง MainApplication 

```
-create MainApplication.class

-add  android:name=".MainApplication"  --> androidmanifest
```

## 3.liberry

* 3.1 เรียกใช้ liberry

```
-" ,':TheCheeseLibrary'  " ->  add library
```

* 3.2 ใช้ Contextor ที่  MainApplication

```
 -MainApp,onCreate --> { Contextor.getInstance().init(getApplicationContext()); }
```

## 4.copy template

* 4.1 ก๊อปปี้ template จาก libarry

```
-singleton -fragment -customview -customviewgroup
```

## 5.create fragment_main

* 5.1 สร้าง fragment เพื่อใช้ แทน activity_main

```
create fragment_main.xml --> layout  xml
```

* 5.2 ก๊อปปี้ template fragmentTemplat เปลี่ยนชื่อเป็น MainFragment

```
create MainFragment.class --> fragment java
```

## 6.add mainfragment to mainactivity 

* 6.1 add fragment เข้าไปที่ activity

-MainActivity.class

```  
  if (savedInstanceState == null){
            getSupportFragmentManager().beginTransaction()
                    .add(R.id.contentContainer, MainFragment.newInstance())
                    .commit();
        }
	 
``` 
-activity_main.xml

``` 
 	  <FrameLayout
            android:id="@+id/contentContainer"
            android:layout_width="match_parent"
            android:layout_height="match_parent"/>

```
# 2.MENU

## 1.change color

* 1. เปลี่ยนสี ที่  ``` values/color ```

## 2.menu

* 2.1 สร้างเมนู ที่ activity_main.xml

/activity_main.xml

 * 2.1 add menu
 
    ```
	 <android.support.v4.widget.DrawerLayout   //ครอบทั้งหมด
	```
	
  * 2.2 เรียกใช้ menu
      
      ```
	<LinearLayout
            android:background="?attr/colorAccent"
            android:layout_gravity="start"
            android:layout_width="@dimen/drawer_menu_width" //ขนาดของเมนูเปลี่ยนเป็น ID
            android:layout_height="match_parent">
        </LinearLayout>
    ```
    
 * 2.3 ทำให้เครื่องขนาดเล็กใช้ได้
 
    ```
   create values-w360dp  = <dimen name="drawer_menu_width">320dp</dimen>
    
                  values = <dimen name="drawer_menu_width">240dp</dimen>
   ```
		      
## 3.Hamburger icon
	
* 3.1 ประกาศ ID ให้ drawerLayout

	```
	 android:id="@+id/drawerLayout"
	```
	
	*  3.2 สร้าง method initInstances(); 
	
	* 3.3 ประกาศตัวแปร  ActionBarDrawerToggle;
	
	```
	ActionBarDrawerToggle actionBarDrawerToggle;
	```
	3.4  ประกาศตัวแปรที่ values/string
	```
	  <string name="open_drawer">Open Menu</string>
	  <string name="close_drawer">Close Menu</string>
	```
	
	* 3.5 new ActionBarDrawerToggle
	```
	    actionBarDrawerToggle = new ActionBarDrawerToggle(
                MainActivity.this,
                binding.drawerLayout,R.string.open_drawer,R.string.close_drawer
        );
       
		
	```
	
	* 3.6 addDrawerListener
	
	```
	 binding.drawerLayout.addDrawerListener(actionBarDrawerToggle);
	```
	
	* 3.6  setHomeButtonEnable 
	
	```
		getSupportActionBar().setHomeButtonEnabled(true);
        getSupportActionBar().setDisplayHomeAsUpEnabled(true);
		
	```
	
	*  3.7 เข้าถึง ActionBar 
	```
	 @Override
    protected void onPostCreate(@Nullable Bundle savedInstanceState) {
        super.onPostCreate(savedInstanceState);
        actionBarDrawerToggle.syncState(); }
	```
	*  3.8 เปลี่ยน icon menu
	```
	 @Override
    public void onConfigurationChanged(Configuration newConfig) {
        super.onConfigurationChanged(newConfig);
        actionBarDrawerToggle.onConfigurationChanged(newConfig);
    }
	```
	 * 3.9 ทำให้ button menu กดได้ 
	
	 ```
	@Override
  	  public boolean onOptionsItemSelected(MenuItem item) {
        if (actionBarDrawerToggle.onOptionsItemSelected(item))
        return true;
        return super.onOptionsItemSelected(item);
    }	 
	```
	 
	 

3#----------------------------------------------------------------
4#----------------------------------------------------------------
5#----------------------------------------------------------------
6#----------------------------------------------------------------

