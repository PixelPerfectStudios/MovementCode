# MovementCode

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class CharController : MonoBehaviour {

    public float speed = 5f;
    public float sensitivity = 5f;
    public float rotateRange = 60f;
    CharacterController player;

    public GameObject eyes;

    float moveWS;
    float moveAD;

    float rotationX;
    float rotationY;

    void Start () 
    {
        player = GetComponent<CharacterController>();
    }
	
    void Update () 
    {
        moveWS = Input.GetAxis("Vertical") * Time.deltaTime * speed;
        moveAD = Input.GetAxis("Horizontal") * Time.deltaTime * speed;

        rotationX = Input.GetAxis("Mouse X") * Time.deltaTime * sensitivity;
        rotationY += Input.GetAxis("Mouse Y") * Time.deltaTime * sensitivity;

        rotationY = Mathf.Clamp(rotationY, -rotateRange, rotateRange);

        Vector3 movement = new Vector3(moveAD, 0, moveWS);
        transform.Rotate(0 , rotationX, 0);
        eyes.transform.localRotation = Quaternion.Euler(rotationY, 0, 0);
        movement = transform.rotation * movement;
        player.Move(movement * Time.deltaTime);
    }
}
```
