# JsonIgnoreProps

This is a tiny helper class to exclude a property from Json Serialization **_when using Newtonsoft.Json_**

In case you have no access to the actual class you're serializing - so you can't add any attributes (like `[JsonIgnore]`), or you simply don't want to. Orif  you would like to decide this at run time - which properties to serialize - then use this class.

Usage:

```csharp
JsonConvert.SerializeObject(
	YourObject,
	new JsonSerializerSettings() {
		ContractResolver = new IgnorePropertiesResolver(new[] { "Prop1", "Prop2" })
	};
);
```

For better performance make sure you *cache* the contractResolver object, do not create it every time.

```csharp
var resolver = new IgnorePropertiesResolver(new[] { "Prop1", "Prop2" });

JsonConvert.SerializeObject(
	YourObject,
	new JsonSerializerSettings() {
		ContractResolver = resolver //reuse
	};
);
```

---
