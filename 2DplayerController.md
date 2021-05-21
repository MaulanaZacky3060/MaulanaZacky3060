using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;

public class PlayerDD : MonoBehaviour
{
    public Slider HP;
    public Collider2D Senjata;
    public bool diTanah = false;
    public Rigidbody2D Player2D;
    public Animator animasiPlayer;
    public float xMove = 0f;
    private float zMove = 0f;
    public float Kecepatan;
    public float LoncatTinggi = 3.0f;
    public float Nyawa = 100f;

    void Update()
    {
        xMove = Input.GetAxisRaw("Horizontal") * Kecepatan;
        zMove = Input.GetAxisRaw("Vertical") * Kecepatan;

        if(Input.GetButton("Horizontal"))
        {
            animasiPlayer.SetFloat("Banter", 1f);
        }

        else{
            animasiPlayer.SetFloat("Banter", 0f);
        }

        if(Nyawa >= 100f)
        {
            Nyawa = 100f;
        }

        if(diTanah == true)
        {
            Loncat();
            Nyerang();
        }

        if(Nyawa <= 0)
        {
            Mati();
        }

        HP.value = Nyawa;

        Player2D.velocity = new Vector2(xMove , Player2D.velocity.y);
    }

    public void Loncat()
    {
        if(Input.GetButton("Jump") && diTanah)
        {
             Player2D.AddForce(transform.up * LoncatTinggi, ForceMode2D.Impulse);
             diTanah = false;
             animasiPlayer.SetBool("Loncat", true);
        }

        else
        {
            animasiPlayer.SetBool("Loncat", false);
        }
       
    }

    void Mati()
    {
         GetComponent<Rigidbody2D>().isKinematic = true;
         animasiPlayer.SetBool("Matek", true);
         Destroy(gameObject, 3);
         Debug.Log("Meninggoy");
    }

    void Nyerang()
    {
        if(Input.GetButtonDown("Fire1"))
        {
            animasiPlayer.SetBool("Nyerangin", true);
        }

        else
        {
            animasiPlayer.SetBool("Nyerangin", false);
        }
    }
}
