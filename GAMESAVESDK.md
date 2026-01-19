layout: page
title: "GAMESAVE SDK"
permalink: /gamesavesdk/

# GameSave SDK for Android

A modern Android save system for Unity and Unreal Engine games, built with Google's DataStore and Kotlin Coroutines.

### Why This SDK?

Unity's PlayerPrefs and basic file I/O have limitations on Android:
- ❌ XML-based (slow for large saves)
- ❌ Can corrupt on app crashes
- ❌ No reactive updates
- ❌ Loads entire save into memory

**GameSave SDK** provides:
- Modern DataStore backend (crash-safe)
- Optimized for frequent reads/writes
- Reactive Flow API for live updates
- Coroutine-based async operations
- Simple integration with Unity

### Installation

Install from: https://assetstore.unity.com/packages/slug/356454

### Using GameSave SDK

```
public class GameManager : MonoBehaviour 
{
    void Start() 
    {
        // 1. Initialize SDK
        GameSaveManager.Initialize();
        
        // 2. Save data
        GameSaveManager.SaveData("player_level", "10");
        
        // 3. Load data
        string level = GameSaveManager.LoadData("player_level");
        Debug.Log($"Player Level: {level}");
    }
}
```

#### That's it! Your saves are now crash-safe and optimized.

### Best Practices

#### Storing Structured Data

Use JSON for complex data structures:
```kotlin
@Serializable
data class PlayerSave(
    val level: Int,
    val experience: Long,
    val inventory: List<String>
)

// Save
val save = PlayerSave(level = 10, experience = 5000, inventory = listOf("sword"))
val json = Json.encodeToString(save)
GameSaveSDK.saveData("player_1", json)

// Load
val json = GameSaveSDK.loadData("player_1")
val save = json?.let { Json.decodeFromString<PlayerSave>(it) }

```

---


### Planned Improvements

**Version 2.0: Encryption**
- Utilize AES-256 encryption to prevent save file tampering/cheating
(Optional change that developers can opt-in)

**Version 3.0: Cloud Sync**
- Firebase backend
- Cross-device sync
- Conflict resolution
- Offline-first

**Version 4.0: Auto-Save System**
- Configurable intervals
- Checkpoints
- Save compression
