---
# 1

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

---
# 1.5

```csharp
using UnityEngine;
using System.Collections;

public class Sheep : MonoBehaviour
{

	[SerializeField]
	Rigidbody2D rb;
	[SerializeField]
	private Vector2 direction;
	[SerializeField]
	float speed;

	Vector2 returnRandomVector() // funkcia pre vypocet random vektoru (smer pohybu ovce)
	{
		float randomX = Random.Range(-1f, 1f);
		float randomY = Random.Range(-1f, 1f);

		direction.x = randomX;
		direction.y = randomY;

		Vector2 normalizedDirection = direction.normalized;

		return normalizedDirection;
	}

	void Start()
	{
		Vector2 normalizedDirection = returnRandomVector(); // passnut variablinu normalizedDirection z funkcie

		rb.linearVelocity = normalizedDirection * speed; // zmena rychlosti pohybu ovce
	}
}
```
