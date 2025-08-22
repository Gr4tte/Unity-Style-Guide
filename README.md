# Unity C# Coding & Project Style Guide

## File Structure
`!Project` - Contains all user created files aside from "Resources" folder
- `Art` - any graphics asset (`sprites`, `animations`, `textures`)
- `Audio`
- `Code`
  - `Scripts`
    - `Debug` - Visalizers and game modifying scripts meant for bug finding and testing
    - `Managers` - Singletons for one scene
    - `Systems` - Persistant Singletons across all scenes
    - `Utils` - static helpers 
    - `UI` - Interactable interfaces
    - `UX` - Effects and feedback
  - `Shaders`

- `Design` - All non graphics, audio or code assets
  - `Scenes`
    - `Dev` - developing but not currently in the game/build
    - `Prod` - included in the build and used in the game
    - `Sandbox` - test and personal scenes to play around in
  - `Prefabs`
  - `Scriptable Objects`
- `Documentation`

## Naming Conventions

### General
- **No abbreviations** unless industry-standard (`AI`, `UI`).
- **Descriptive but concise**. Don’t repeat class name in variable names.
  ```csharp
  // ❌ Avoid
  [SerializeField] private float _characterSpeed;
  
  // ✅ Do
  [SerializeField] private float _speed;
### Classes
  - `PascalCase`
  - **Scriptable Objects** end with `SO`
    ```csharp
    public class EnemySO : ScriptableObject { }
  - **Singletons**
    - **Normal** ends with `Manager`
    - **Persistant** ends with `System`
    ```csharp
    public class EntityManager : Singleton<EntityManager> { }
    public class AudioSystem : PersistantSingleton<AudioSystem > { }
### Interfaces
  - `PascalCase`
  - Prefixed by `I`
	  ```csharp
	  public interface IWeapon { }
### Methods
  - `PascalCase`
  - Start with a verb
	  ```csharp
	  private void DoSomething() { }
	public int GetHealth() { return _health; }
### Fields, Properties and Variables
  - **Private**
    - `camelCase` 
    - prefixed by `_`
    ```csharp
    private int _health;
  - **Inspector Editable**
    - `camelCase` 
    - prefixed by `_`
    - using `SerializeField` attribute
    ```csharp
    [SerializeField] private float _speed;
  - **Public fields/properties**
    - `PascalCase` 
    - Using `field: SerializeField` if inspector editable
    - Avoid public setters
    ```csharp
    public int Health { get; private set; }
    [field: SerializeField] public int Health { get; private set; }
  - **Scoped variables**
    - `camelCase` 
    ```csharp
    int localCounter = 0;
  - **Constants**
    - `UPPER_CASE` 
    - use a serialized field instead when possible
    ```csharp
	private const int MAX_ENTITIES = 100;
### Booleans
  - prefix with (`is`, `has`, `can`, etc)
  - keep positive
	  ```csharp
	  // ❌ Avoid  
	 public bool Grounded { get; private set; }
	 private bool _isDead
	  
	  // ✅ Do  
	 public bool IsGrounded { get; private set; }
	 private bool _isAlive;
### Booleans
  - always plural
	  ```csharp
	private List<int> _numbers;
	private string[] _names;
## Unity Specific
  - `Awake` - cache reference (don't call another class' methods or fields)
  - `Start` - initialization requiring another class' methods and fields
  - `Update` - gameplay loop 
    - Avoid `FindObjectOfType` or `GetComponent`
    - Avoid code other than method calls
  - 
