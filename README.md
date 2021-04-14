# SettingsFragment

## Ejemplo en el que se utiliza un Fragmento para mostrar los ajustes.

Enlaces relacionados:

[https://developer.android.com/guide/navigation/navigation-global-action](https://developer.android.com/guide/navigation/navigation-global-action)

[https://developer.android.com/codelabs/android-navigation](https://developer.android.com/codelabs/android-navigation)

[https://stackoverflow.com/questions/53029821/navigating-to-preference-fragment-using-navigation-component](https://stackoverflow.com/questions/53029821/navigating-to-preference-fragment-using-navigation-component)

Si se puede acceder al fragmento de ajustes desde más de un fragmento, se debe agregar en el editor de navegación como una acción global.

### Icono para volver a la actividad anterior

Para habilitar en la barra de acción del fragmento de ajustes el icono para volver a la actividad "padre":

>@Override  
public void onCreatePreferences(Bundle savedInstanceState, String rootKey) {  
 ActionBar actionBar;  
 actionBar = ((AppCompatActivity)getActivity()).getSupportActionBar();  
 **actionBar.setDisplayHomeAsUpEnabled(true);**  
 ...  
}

Para responder a la pulsación sobre el icono de vuelta a la actividad "padre" se ha de implementar en la actividad que contiene al fragmento:

>@Override  
public boolean onOptionsItemSelected(MenuItem item) {  
 int id = item.getItemId();  
 **if (id == android.R.id.home) {  
  onBackPressed();  
 }**  
 ...  
 return super.onOptionsItemSelected(item);  
}

Una vez que en el fragmento de ajustes se ha habilitado el icono de vuelta a la actividad "padre", el icono se queda visible, por lo que será necesario ocultarlo
en todos los fragmentos desde los que se puede llegar al fragmento de ajustes:

>public void onViewCreated(@NonNull View view, Bundle savedInstanceState) {  
 super.onViewCreated(view, savedInstanceState);  
 ActionBar actionBar;  
 actionBar = ((AppCompatActivity)getActivity()).getSupportActionBar();  
 **actionBar.setDisplayHomeAsUpEnabled(false);**  
 ...  
}

### Deshabilitar el menú en el fragmento de ajustes

Para deshabilitar el menú del fragmento de ajustes en el propio fragmento de ajustes:

>@Override
public void onCreate(@Nullable Bundle savedInstanceState) {  
 super.onCreate(savedInstanceState);  
 **setHasOptionsMenu(true);**  
}  

>@Override  
public void onCreateOptionsMenu(@NonNull Menu menu, @NonNull MenuInflater inflater) {  
 super.onCreateOptionsMenu(menu, inflater);  
 **menu.clear();**  
}  
