# Thief! C#

This program that displays all the possible combinations for any four numerical digits entered by the user. The program should avoid displaying the same
combination more than once.


    using System;
    using System.Collections.Generic;
    using System.ComponentModel;
    using System.Data;
    using System.Drawing;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Windows.Forms;
    
    namespace Thief_
    {
        public partial class Form1 : Form
        {
            public Form1()
            {
                InitializeComponent();
                listBoxdigits.Hide();
            }
    
            private void Form1_Load(object sender, EventArgs e)
            {
    
            }
    
            private void pin_generator_Click(object sender, EventArgs e)
            {
                listBoxdigits.Items.Clear();// Clear the ListBox 
    
                string raw_pin = Pin.Text;
                if (raw_pin.Length == 4)// Checks if the input is exactly 4 digits
                {
                    char[] digits = raw_pin.ToCharArray();// place the input string into an array digits
                    List<string> combinations = new List<string>();// makes a new list called combinations that can hold multiple string values
    
                    GenerateCombinations(digits, 0, combinations);// Generate all combinations
    
                    foreach (string combination in combinations)// Add each combination to the ListBoxdigits
                    {
                        listBoxdigits.Items.Add(combination);
                    }
                    listBoxdigits.Show();
    
                }
                else { error_message.Text = "Invalid Pincode, Please Enter 4 DIGITS"; Pin.Text = ""; } 
            }
    
            private void GenerateCombinations(char[] digits, int index, List<string> combinations) 
            {
                if (index == digits.Length - 1)//checks if the index variable has reached the last position in the digits array
                {
                    string combination = new string(digits);//turns the character array into a string called combination
                    if (!combinations.Contains(combination)) // This line checks if the newly formed combination string is already in the combinations list
                    {
                        combinations.Add(combination);
                    }
                    return;
                }
    
                for (int i = index; i < digits.Length; i++)// goes through the digits array starting from the current index position to the end of the array
                {
                    Swap(digits, index, i);// swaps the digit at the index position with the digit at position i
                    GenerateCombinations(digits, index + 1, combinations);//moves to the next position and continues the process of swapping and finding combinations
                    Swap(digits, index, i); // Swap back to original places
                }
            }
            private void Swap(char[] array, int i, int x)
            {
                char temp_array = array[i];//holds the value of the element at index i in the array
                array[i] = array[x];//element at index x is assigned to the element at index i
                array[x] = temp_array;
            }
    
            private void listBoxdigits_SelectedIndexChanged(object sender, EventArgs e)
            {
    
            }
            
        }
    }
