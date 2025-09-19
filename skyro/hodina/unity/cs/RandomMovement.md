```csharp
using UnityEngine;
using System.Collections;

/*
tento kod robi to ze ked zapnem hru, tak sa objekt pohne niakym smerom
*/

public class Sheep : MonoBehaviour
{

	[SerializeField]
	Rigidbody2D rb; // definuj Rigidbody2D ako "rb"

	[SerializeField]
	private Vector2 direction; // povedz ze direction je Vector2

	void Start()
	{
		rb.linearVelocity = direction;
	}

}
```
