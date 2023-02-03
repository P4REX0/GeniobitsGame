using System.Collections;
using UnityEngine;
using UnityEngine.UI;
using TMPro;

public class SpinManager : MonoBehaviour
{
    //Private Variables
    private int randValue;
    private float timeInterval;
    private bool isSpining;
    private int finalAngle;
    private string PlayerInput;
    private float totalAngle;

    //Public Variabels
    [Header("Wheel Variables")]
    public float Timer = 60f;
    public int Sections;
    public GameObject ResultPanel;
    public TextMeshProUGUI TimerTxt;
    public TextMeshProUGUI ResultTxt;
    public TextMeshProUGUI PrizeNumber;
    public TextMeshProUGUI SelectedNumber;

    [SerializeField] private Button[] Btn; // All Buttons reference
    [SerializeField] private string[] PrizeName; 

    private void Start()
    {
        isSpining = true;
        totalAngle = 360 / Sections;
    }

    private void Update()
    {
        if (!isSpining) return;

        Timer -= Time.deltaTime;
        TimerTxt.text = "Timer : " + (int)Timer;
        if (Timer <= 0  )
        {
            isSpining = false;
            StartCoroutine(spin(PlayerInput));
            Timer = 60f;
        }
    }

    private IEnumerator spin(string input)
    {
        randValue = Random.Range(200, 300);

        timeInterval = 0.00001f * Time.deltaTime * 2;

        // To Rotate Wheel 
        for (int i = 0; i < randValue; i++)
        {
            transform.Rotate(0, 0, (totalAngle / 2));

            if (i > Mathf.RoundToInt(randValue * 0.2f))
                timeInterval = 0.5f * Time.deltaTime;
            if (i > Mathf.RoundToInt(randValue * 0.2f))
                timeInterval = 1f * Time.deltaTime;
            if (i > Mathf.RoundToInt(randValue * 0.2f))
                timeInterval = 1.5f * Time.deltaTime;
            if (i > Mathf.RoundToInt(randValue * 0.2f))
                timeInterval = 2f * Time.deltaTime;
            if (i > Mathf.RoundToInt(randValue * 0.2f))
                timeInterval = 2.5f * Time.deltaTime;

            yield return new WaitForSeconds(timeInterval);
        }

        if (Mathf.RoundToInt(transform.eulerAngles.z) % totalAngle != 0)
        {
            transform.Rotate(0, 0, (totalAngle / 2));
        }

        finalAngle = Mathf.RoundToInt(transform.eulerAngles.z);
        print(finalAngle);

        //To Check result
        for (int i = 0; i < Sections; i++)
        {
            if (finalAngle == i * totalAngle)
            {
                PrizeNumber.text = PrizeName[i]; 

                if (input == PrizeName[i])
                {
                    ResultPanel.SetActive(true);
                    ResultTxt.text = "You Won";
                }  
                else
                {
                    ResultPanel.SetActive(true);
                    ResultTxt.text = "You Lose";
                }
                SetButton(true);
            }
        }
    }

    //Getting Input From User
    public void ButtonInput(string input)
    {
        ResultTxt.text = "";
        SelectedNumber.text = input;
        SetButton(false);
        PlayerInput = input;
    }

    //Function for replay Game
    public void RestartBtn()
    {
        isSpining = true;
    }

    private void SetButton(bool val)
    {
        for (int i = 0; i < Btn.Length; i++)
        {
            Btn[i].GetComponent<Button>().interactable = val;
        }
    }
}
