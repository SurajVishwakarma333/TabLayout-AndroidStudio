# TabLayout-Android Studio

Lets create a Tab Layout in android app.

**Step 1 : Create a new project in Android Studio, go to File ⇒ New Project and fill all required details to create a new project.**

**Step 2 : Add the following dependency to create a tab layout**

      implementation 'com.android.support:design:28.0.0'
  
**Step 3 − Add the following code to res/layout/activity_main.xml.**

      <?xml version="1.0" encoding="utf-8"?>
      <RelativeLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".MainActivity">
        
        <android.support.design.widget.TabLayout
          android:id="@+id/tabLayout"
          android:layout_width="match_parent"
          android:layout_height="wrap_content"
          android:background="#1db995">
        </android.support.design.widget.TabLayout>
        
        <android.support.v4.view.ViewPager
          android:id="@+id/viewPager"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:layout_below="@id/tabLayout"
          android:layout_centerInParent="true"
          android:layout_marginTop="100dp"
          tools:layout_editor_absoluteX="8dp" />
       </RelativeLayout>

**Step 4 − Add the following code to src/MainActivity.java**

      import android.support.v7.app.AppCompatActivity;
      import android.os.Bundle;
      import android.support.design.widget.TabLayout;
      import android.support.v4.view.ViewPager;
      public class MainActivity extends AppCompatActivity {
       TabLayout tabLayout;
       ViewPager viewPager;
      @Override
      protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        
        tabLayout = findViewById(R.id.tabLayout);
        viewPager = findViewById(R.id.viewPager);
        tabLayout.addTab(tabLayout.newTab().setText("Football"));
        tabLayout.addTab(tabLayout.newTab().setText("Cricket"));
        tabLayout.addTab(tabLayout.newTab().setText("NBA"));
        tabLayout.setTabGravity(TabLayout.GRAVITY_FILL);
      
       final MyAdapter adapter = new MyAdapter(this,getSupportFragmentManager(),
       tabLayout.getTabCount());
       viewPager.setAdapter(adapter);
       viewPager.addOnPageChangeListener(new TabLayout.TabLayoutOnPageChangeListener(tabLayout));
       tabLayout.addOnTabSelectedListener(new TabLayout.OnTabSelectedListener() {
           @Override
           public void onTabSelected(TabLayout.Tab tab) {
             viewPager.setCurrentItem(tab.getPosition());
           }
           @Override
           public void onTabUnselected(TabLayout.Tab tab) {
           }
           @Override
           public void onTabReselected(TabLayout.Tab tab) {
           }
        });
       }
      }
      
**Step 5 – Create a java class(MyAdapter.java) and add the following code**

      import android.content.Context;
      import android.support.v4.app.Fragment;
      import android.support.v4.app.FragmentPagerAdapter;
      import android.support.v4.app.FragmentManager;
      class MyAdapter extends FragmentPagerAdapter {
       Context context;
       int totalTabs;
      public MyAdapter(Context c, FragmentManager fm, int totalTabs) {
      super(fm);
      context = c;
      this.totalTabs = totalTabs;
      }
      @Override
      public Fragment getItem(int position) {
         switch (position) {
           case 0:
              Football footballFragment = new Football();
              return footballFragment;
           case 1:
              Cricket cricketFragment = new Cricket();
              return cricketFragment;
           case 2:
              NBA nbaFragment = new NBA();
              return nbaFragment;
              default:
              return null;
             }
           }
        @Override
        public int getCount() {
        return totalTabs;
        }
       }
       
**Step 6 – Now create the fragments and the layouts (Right click on the project >> New >> Fragment >> Blank**

> a) FootBall.java

      import android.os.Bundle;
      import android.support.v4.app.Fragment;
      import android.view.LayoutInflater;
      import android.view.View;
      import android.view.ViewGroup;
      public class Football extends Fragment {
       public Football() {
       // Required empty public constructor
       }
      @Override
       public View onCreateView(LayoutInflater inflater, ViewGroup container,
       Bundle savedInstanceState) {
       return inflater.inflate(R.layout.fragment_football, container, false);
       }
      }
      
**fragment_football.xml**

     <?xml version="1.0" encoding="utf-8"?>
     <FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:tools="http://schemas.android.com/tools"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      tools:context=".Football">
      <!-- TODO: Update blank fragment layout -->
      <TextView
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:textAlignment="center"
            android:text="Football Fragment"
            android:textSize="16sp"
            android:textStyle="bold"/>
     </FrameLayout>
      
      
> b) Cricket.java


      import android.os.Bundle;
      import android.support.v4.app.Fragment;
      import android.view.LayoutInflater;
      import android.view.View;
      import android.view.ViewGroup;
      public class Cricket extends Fragment {
       public Cricket() {
      // Required empty public constructor
       }
      @Override
       public View onCreateView(LayoutInflater inflater, ViewGroup container,
       Bundle savedInstanceState) {
       return inflater.inflate(R.layout.fragment_cricket, container, false);
       }
      } 
      
      
**fragment_cricket.xml**


     <?xml version="1.0" encoding="utf-8"?>
     <FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:tools="http://schemas.android.com/tools"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      tools:context=".Cricket">
      <TextView
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:textAlignment="center"
            android:text="Cricket Fragment"
            android:textSize="16sp"
            android:textStyle="bold"/>
     </FrameLayout>
      
      
> c) NBA.java


      import android.os.Bundle;
      import android.support.v4.app.Fragment;
      import android.view.LayoutInflater;
      import android.view.View;
      import android.view.ViewGroup;
      public class NBA extends Fragment {
       public NBA() {
       // Required empty public constructor
       }
       @Override
       public View onCreateView(LayoutInflater inflater, ViewGroup container,
       Bundle savedInstanceState) {
       return inflater.inflate(R.layout.fragment_nb, container, false);
       }
      }
      
      
**fragment_nba.xml**


     <?xml version="1.0" encoding="utf-8"?>
     <FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:tools="http://schemas.android.com/tools"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      tools:context=".NBA">
      <!-- TODO: Update blank fragment layout -->
      <TextView
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:textAlignment="center"
            android:text="NBA Fragment"
            android:textSize="16sp"
            android:textStyle="bold"/>
     </FrameLayout>
      
     



https://user-images.githubusercontent.com/101108540/173747133-d6f431aa-add5-4b1a-8f0e-551c2f3515d4.mp4

