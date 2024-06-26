
#  Cocktail App with Coroutines,Retrofit and Shared Preferences

This is a simple Android app that demonstrates the Model-View-ViewModel (MVVM) architectural pattern while using Coroutines and Retrofit to fetch and display data from TheCocktailDB API, and sharedPreferences.

### Shared Prefs Example
```kt

class SharedPrefs(context: Context) {
    private val preferences: SharedPreferences? =
        context.getSharedPreferences("FavoriteStatus", Context.MODE_PRIVATE)

    fun addFavorite(cocktail: CocktailModel) {
        val favorites = getFavorites()
        favorites.add(cocktail)
        saveFavorites(favorites)
    }

    fun removeFavorite(cocktail: CocktailModel) {
        val favorites = getFavorites()
        favorites.remove(cocktail)
        saveFavorites(favorites)
    }

    // defvalue is the default value if the key is not found in the shared preferences
    // in this case, we are returning an empty list if the key is not found
    fun getFavorites(): MutableList<CocktailModel> {
        val json = preferences?.getString("favorites", "[]")
        val favorites = Gson().fromJson(json, Array<CocktailModel>::class.java)
        return favorites?.toMutableList() ?: mutableListOf()
    }

    private fun saveFavorites(favorites: List<CocktailModel>) {
        val json = Gson().toJson(favorites)
        preferences?.edit()?.putString("favorites", json)?.apply()
    }
}
```

## Features
- Get favorite cocktail list from shared preferences.
- Fetches and displays a list of movies from the CocktailDB API.
- Implements MVVM architecture for clean and maintainable code.
- Utilizes Coroutines for asynchronous operations.
- Uses Retrofit for making network requests.
## Todo Features
- Search Bar.
- Cocktail Details page that includes ingredients.
- UI update
## Screenshots
</br>

| Feed Screen | Favorites Screen |
| ------- | ------- | 
|<img src="Screenshot_20231122_231243.png" width="250" height="500"/>|<img src="Screenshot_20231122_231319.png" width="250" height="500"/>|

</br>

## Libraries Used
- Coroutines for managing asynchronous tasks.
- Retrofit for making API requests.
- Glide for loading and caching images.
- ViewModel from Android Architecture Components.
- LiveData for reactive data updates.

## Installation
Clone the repository:

Copy code
```bash
 git clone https://github.com/Kochipek/CocktailsApp.git

```
Open the project in Android Studio.

Build and run the app on an Android emulator or a physical device.

## Usage
- The app displays a list of Cocktails
- Click star button to add favorite the cocktail you like
- Navigate to Favorites screen from botton bar to get a list of your favorite Cocktails!
