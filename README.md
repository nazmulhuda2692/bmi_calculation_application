// Flutter framework ইমপোর্ট করা হচ্ছে
import 'package:flutter/material.dart';

// অ্যাপ চালু করার জন্য main function
void main() {
  // Flutter অ্যাপ রান করানো হচ্ছে
  runApp(MyApp());
}

// মূল অ্যাপ ক্লাস
class MyApp extends StatelessWidget {
  // Widget build করার method
  @override
  Widget build(BuildContext context) {
    // MaterialApp রিটার্ন করা হচ্ছে
    return MaterialApp(
      // অ্যাপের title
      title: 'BMI Calculator',

      // Debug banner বন্ধ করা হয়েছে
      debugShowCheckedModeBanner: false,

      // অ্যাপের theme সেট করা হয়েছে
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),

      // Home page সেট করা হয়েছে
      home: BMIScreen(),
    );
  }
}

// Stateful Widget কারণ BMI calculate করার পর UI পরিবর্তন হবে
class BMIScreen extends StatefulWidget {
  @override
  _BMIScreenState createState() => _BMIScreenState();
}

// State class তৈরি করা হয়েছে
class _BMIScreenState extends State<BMIScreen> {

  // Height input নেওয়ার জন্য controller
  TextEditingController heightController = TextEditingController();

  // Weight input নেওয়ার জন্য controller
  TextEditingController weightController = TextEditingController();

  // BMI result রাখার জন্য variable
  double bmi = 0;

  // BMI status রাখার জন্য variable
  String result = "";

  // BMI calculate করার function
  void calculateBMI() {

    // Height input String থেকে double এ convert করা হচ্ছে
    double height = double.parse(heightController.text);

    // Weight input String থেকে double এ convert করা হচ্ছে
    double weight = double.parse(weightController.text);

    // Height কে meter এ convert করা হচ্ছে
    double heightMeter = height / 100;

    // BMI formula প্রয়োগ করা হচ্ছে
    double bmiResult = weight / (heightMeter * heightMeter);

    // UI update করার জন্য setState ব্যবহার করা হচ্ছে
    setState(() {

      // BMI value update করা হচ্ছে
      bmi = bmiResult;

      // BMI range অনুযায়ী result নির্ধারণ করা হচ্ছে
      if (bmi < 18.5) {
        result = "Underweight";
      } else if (bmi >= 18.5 && bmi < 24.9) {
        result = "Normal Weight";
      } else if (bmi >= 25 && bmi < 29.9) {
        result = "Overweight";
      } else {
        result = "Obese";
      }
    });
  }

  // UI design করার method
  @override
  Widget build(BuildContext context) {

    // Main Scaffold widget
    return Scaffold(

      // AppBar তৈরি করা হয়েছে
      appBar: AppBar(
        title: Text("BMI Calculator"),
      ),

      // Body section তৈরি করা হয়েছে
      body: Padding(

        // চারপাশে padding দেওয়া হয়েছে
        padding: const EdgeInsets.all(16.0),

        // Column ব্যবহার করে widget গুলো vertical ভাবে সাজানো হয়েছে
        child: Column(

          // Widget গুলো center এ রাখা হয়েছে
          mainAxisAlignment: MainAxisAlignment.center,

          children: [

            // Height input field
            TextField(

              // Height controller যুক্ত করা হয়েছে
              controller: heightController,

              // শুধুমাত্র number keyboard দেখানো হবে
              keyboardType: TextInputType.number,

              // Input decoration দেওয়া হয়েছে
              decoration: InputDecoration(
                labelText: "Enter Height (cm)",
                border: OutlineInputBorder(),
              ),
            ),

            // দুই widget এর মাঝে space
            SizedBox(height: 20),

            // Weight input field
            TextField(

              // Weight controller যুক্ত করা হয়েছে
              controller: weightController,

              // শুধুমাত্র number keyboard দেখানো হবে
              keyboardType: TextInputType.number,

              // Input decoration দেওয়া হয়েছে
              decoration: InputDecoration(
                labelText: "Enter Weight (kg)",
                border: OutlineInputBorder(),
              ),
            ),

            // Space দেওয়া হয়েছে
            SizedBox(height: 20),

            // BMI calculate button
            ElevatedButton(

              // Button press করলে calculateBMI function call হবে
              onPressed: calculateBMI,

              // Button এর text
              child: Text("Calculate BMI"),
            ),

            // Space দেওয়া হয়েছে
            SizedBox(height: 20),

            // BMI result দেখানো হচ্ছে
            Text(

              // BMI value দুই দশমিক পর্যন্ত দেখানো হচ্ছে
              "BMI: ${bmi.toStringAsFixed(2)}",

              // Text style
              style: TextStyle(
                fontSize: 24,
                fontWeight: FontWeight.bold,
              ),
            ),

            // Space দেওয়া হয়েছে
            SizedBox(height: 10),

            // BMI status দেখানো হচ্ছে
            Text(

              // Result text
              result,

              // Text style
              style: TextStyle(
                fontSize: 22,
                color: Colors.green,
              ),
            ),
          ],
        ),
      ),
    );
  }
}
