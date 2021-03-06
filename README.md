# 1.mvc structure
## 1.1.binding

* 1.1 เรียกใช้  binding

#### app/gradle

```
 dataBinding{enabled true}
```

## 1.2.mvc

* 2.1 สร้าง package รูปแบบ MVC

#### /java/package

```
# activity
# manager
# util
# view 
# fragment
```
* 1.2.2 สร้าง MainApplication.java 

#### java/app

-create 
```
MainApplication.java
```

* 1.2.3 add MainApplication
#### androidmanifest.xml

```
 android:name=".MainApplication"
```

## 1.3.library

* 1.3.1 เรียกใช้ library
#### settings.gradle
```
 ,':TheCheeseLibrary'  
 
```
   * 1.3.1.1  add library เข้า ไปใน app
   #### app/gradle
   
   ```
   
   implementation project(':TheCheeseLibrary')
   
   ```

* 1.3.2 ใช้ Contextor ที่  MainApplication

#### MainApplication.java 
```

  Contextor.getInstance().init(getApplicationContext()); 
 
```

## 1.4.copy template

* 1.4.1 ก๊อปปี้ template จาก libarry

#### manager

- singletontemplate.java

#### fragment

- fragmenttemplate.java

#### view

- customviewtemplate.java

- customviewgrouptemplate.java

## 1.5.create fragment_main


* 1.5.1 สร้าง fragment เพื่อใช้ แทน activity_main

#### res/layout

create
 - fragment_main.xml 


* 5.2 ก๊อปปี้ template fragmentTemplat เปลี่ยนชื่อเป็น MainFragment

#### fragment

create
 - MainFragment.java


## 1.6.add mainfragment to mainactivity 

* 1.6.1 add fragment เข้าไปที่ activity

#### activity_main.xml

``` 
 	  <FrameLayout
            android:id="@+id/contentContainer"
            android:layout_width="match_parent"
            android:layout_height="match_parent"/>

```

#### MainActivity.class

```  
  if (savedInstanceState == null){
            getSupportFragmentManager().beginTransaction()
                    .add(R.id.contentContainer, MainFragment.newInstance())
                    .commit();
        }
	 
``` 

# 2.MENU

## 2.1.change color 

* 2.1.1. เปลี่ยนสี 
#### values/color

## 2.2.menu

* 2.2.1 สร้างเมนู ที่ activity_main.xml

#### activity_main.xml

 * 2.2.3 add menu
 
    ```
	 <android.support.v4.widget.DrawerLayout   //ครอบทั้งหมด
	```
	
  * 2.2.4 เรียกใช้ menu
      
      ```
	<LinearLayout
            android:background="?attr/colorAccent"
            android:layout_gravity="start"
            android:layout_width="@dimen/drawer_menu_width" //ขนาดของเมนูเปลี่ยนเป็น ID
            android:layout_height="match_parent">
        </LinearLayout>
    ```
    
 * 2.2.5 ทำให้เครื่องขนาดเล็กใช้ได้
 
    ```
   create values-w360dp  = <dimen name="drawer_menu_width">320dp</dimen>
    
                  values = <dimen name="drawer_menu_width">240dp</dimen>
   ```
		      
# 3.Hamburger icon

### 3.1. ประกาศ ID
#### activity_main.xml
* 3.1.1 ประกาศ ID ให้ drawerLayout

	```
	 android:id="@+id/drawerLayout"
	```
## 3.2. add Hamburger
#### MainActivity.java	
* 3.2.1 สร้าง method initInstances(); 
	
* 3.2.2 ประกาศตัวแปร  ActionBarDrawerToggle;
	
	```
	ActionBarDrawerToggle actionBarDrawerToggle;
	```
####  values/string.xml
* 3.2.3  ประกาศตัวแปรที่ values/string
	```
	  <string name="open_drawer">Open Menu</string>
	  <string name="close_drawer">Close Menu</string>
	```
#### MainActivity.java	
* 3.3.4 new ActionBarDrawerToggle
	```
	    actionBarDrawerToggle = new ActionBarDrawerToggle(
                MainActivity.this,
                binding.drawerLayout,R.string.open_drawer,R.string.close_drawer
        );
       
		
	```
	
* 3.3.5 addDrawerListener
	
	```
	 binding.drawerLayout.addDrawerListener(actionBarDrawerToggle);
	```
	
* 3.3.6  setHomeButtonEnable 
	
	```
		getSupportActionBar().setHomeButtonEnabled(true);
        getSupportActionBar().setDisplayHomeAsUpEnabled(true);
		
	```
	
*  3.3.7 เข้าถึง ActionBar 
	```
	 @Override
    protected void onPostCreate(@Nullable Bundle savedInstanceState) {
        super.onPostCreate(savedInstanceState);
        actionBarDrawerToggle.syncState(); }
	```
*  3.3.8 เปลี่ยน icon menu
	```
	 @Override
    public void onConfigurationChanged(Configuration newConfig) {
        super.onConfigurationChanged(newConfig);
        actionBarDrawerToggle.onConfigurationChanged(newConfig);
    }
	```
 * 3.3.9 ทำให้ button menu กดได้ 
	
	 ```
	@Override
  	  public boolean onOptionsItemSelected(MenuItem item) {
        if (actionBarDrawerToggle.onOptionsItemSelected(item))
        return true;
        return super.onOptionsItemSelected(item);
    }	 
	```
	 
	 

# 4. ToolBar
## 4.1.ซ้อน actionbar
#### values/styles

 ```
 <style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
	
 ```
 
## 4.2 แปะ toolbar เข้าไป layout
  * 4.2.1 ครอบ FrameLayout ด้วย LinearLayout  
  	* และใช้ Toolbar แล้วประกาศ ID แล้วใส่ background และเปลี่ยน theme แล้ว popuptheme
  #### activity_main.xml
  ```
  <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:orientation="vertical">

            <android.support.v7.widget.Toolbar
                android:id="@+id/toolbar"
                android:layout_width="match_parent"
                android:layout_height="?attr/actionBarSize"
                android:background="?attr/colorPrimary"
                android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar"
		android:popupTheme="@style/ThemeOverlay.AppCompat.Light"/>

            <FrameLayout
                android:id="@+id/contentContainer"
                android:layout_width="match_parent"
                android:layout_height="match_parent" />
        </LinearLayout>
``` 
 * 4.2.2 บอก actionbarว่าจะ ใช้ toolbar แทน
  #### MainActivity.java/initInstances()
  ```
  setSupportActionBar(binding.toolbar);
   ```

# 5.สร้าง layout เพื่อใช้เป็น CustomViewGroup 
 #### layout
 
 list_item_photo.xml
 

 
 * 5.1 ใช้ CustomViewGroupTemplate ทำเป็น  PhotoListItem
  #### java/view/PhotoListItem.java 
  * binding inflater
   ```
    private void initInflate() {
        LayoutInflater inflater = (LayoutInflater) getContext().getSystemService(Context.LAYOUT_INFLATER_SERVICE);
        binding = ListItemPhotoBinding.inflate(inflater, this, true);
    }
```
  * 5.1.1 ทำให้ CustomViewGroup มีขนาด 2/3
 ```
  @Override
    protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
        int width = MeasureSpec.getSize(widthMeasureSpec);
        int height = width * 2 / 3;
        int newHeightMeasureSpec = MeasureSpec.makeMeasureSpec(
                height,
                MeasureSpec.EXACTLY
        );
        // Child Views
        super.onMeasure(widthMeasureSpec, newHeightMeasureSpec);
        // Self
        setMeasuredDimension(width,height);
    }
 ```
 
 
 	
# 6.ListView	
 ## 6.1 แปะ listview ไปที่  fragment_main
#### fragment_main.xml
 ``` 
      <ListView
           android:id="@+id/listView"
           android:layout_width="match_parent"
           android:layout_height="match_parent">

       </ListView>
 ```
 ## 6.2 สร้าง package adapter เพื่อส่ง view ให้ listview
 	* 6.2.1สร้าง PhotoListAdapter.java และ  extends BaseAdapter
	
```
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        PhotoListItem item;
        if ( convertView != null)
                item = (PhotoListItem) convertView;
        else
            item = new PhotoListItem(parent.getContext());
        return  item;
    }
```
   * ถ้ามี view มากว่า 1 ประเภทใน listview
```
    @Override
    public int getViewTypeCount() {
        return 2;
    }

    @Override
    public int getItemViewType(int position) {
        return position % 2 == 0 ? 0 : 1;
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        if (getItemViewType(position) == 0) {
            PhotoListItem item;
            if (convertView != null)
                item = (PhotoListItem) convertView;
            else
                item = new PhotoListItem(parent.getContext());
            return item;
        } else {
            TextView item;
            if (convertView != null)
                item = (TextView) convertView;
            else
                item = new TextView(parent.getContext());
            item.setText("Position: " + position);
            return item;
        }
```
	
## 6.3 new PhotoListAdapter ที่ MianFragment และ set Adapter ให้ list view
#### fragment/MainFragment.java/initInstances()
```
  listAdapter = new PhotoListAdapter();
   binding.listView.setAdapter(listAdapter);
```
   * 6.3.1 onCreateView สำหรับ binding
```
 @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        binding = DataBindingUtil.inflate(
                inflater, R.layout.fragment_main, container, false);
        View rootView = binding.getRoot();
        initInstances(rootView);
        return rootView;
    }
  ```
# 7.  DAO
#### Server = JSON -> retrofit = string ->  Converter = DAO -> DAO
 ## 7.1 ติดตั้ง retrofit Library
 http://square.github.io/retrofit/
#### app/gradle
  ```
 implementation 'com.squareup.retrofit2:retrofit:2.4.0'
  ```
 ## 7.2 ประกาศ interface  
#### manager/http/ApiService.java 
https://nuuneoi.com/courses/500px/list
  ```
public interface ApiService {
    @POST("list")
    Call<Object> loadPhotoList();
}
  ```
  ## 7.3 สร้าง retrofit  สร้างด้วย SingletonTemplate  ตั้งชื่อว่า HttpManager
  #### manager/HttpManager.java
   ```
      private ApiService service;
    private HttpManager() {
        mContext = Contextor.getInstance().getContext();
        Retrofit retrofit = new Retrofit.Builder()
                .baseUrl("https://nuuneoi.com/courses/500px/")
                .build();
        service = retrofit.create(ApiService.class);
    }

    public ApiService getService() {
        return service;
    }
 ```
 ## 7.4 ติดตั้ง  Converter
 #### app/gradle
 ```
  implementation 'com.squareup.retrofit2:converter-gson:2.4.0'
  ```
   * ใส่ Converter ให้ retrofit
   
   #### manager/HttpManager.java
    
```
	.baseUrl("https://nuuneoi.com/courses/500px/")
	  
       .addConverterFactory(GsonConverterFactory.create())
       
        .build();
```
## 7.5 สร้าง DAO
 
   * สร้าง package dao 
  	* ประกาศตัวแปรจากข้างในออกข้างนอก
  	* 7.5.1 สร้าง PhotoItemDao.java  
	#### DAO/PhotoItemDao.java  
	* ประกาศตัวแปรข้างใน แล้วให้ android studio generate get set ให้
	
https://nuuneoi.com/courses/500px/list
	
Ex. ตัวอย่าง DAO  

```
    @SerializedName("id")        private  int id;
    @SerializedName("link")      private String link;
    @SerializedName("image_url") private String imageUrl;
    .
    .
    n
    
    public int getId() { return id; }
    public void setId(int id) { this.id = id; }
    public String getLink() { return link; }
    public void setLink(String link) { this.link = link; }
    public String getImageUrl() { return imageUrl; }
    public void setImageUrl(String imageUrl) { this.imageUrl = imageUrl; }  
    .
    .
    n
```
* 7.5.2 สร้าง PhotoItemCollectionDao.java
#### DAO/PhotoItemCollectionDao.java  
* ประกาศตัวแปรข้างนอก แล้วให้ android studio generate get set ให้ 
* ใส่ PhotoItemDao ใน List<PhotoItemDao> data
	
```
public class PhotoItemCollectionDao {
    @SerializedName("success") private boolean success;
    @SerializedName("data") private List<PhotoItemDao> data;  

    public boolean isSuccess() { return success; }
    public void setSuccess(boolean success) { this.success = success; }
    public List<PhotoItemDao> getData() {return data; }
    public void setData(List<PhotoItemDao> data) { this.data = data; }
}
```
 * 7.5.3 PhotoItemCollectionDao แปะที่ ApiService
 #### manager/http/ApiService.java 
 ```
public interface ApiService {
    @POST("list")
    Call<PhotoItemCollectionDao> loadPhotoList();
}
  ```
			
