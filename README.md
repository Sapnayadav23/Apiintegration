import 'dart:convert';
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'package:http/http.dart';
import 'package:secondproject/Models/post_model.dart';

class Login extends StatefulWidget {
  const Login({super.key});

  @override
  State<Login> createState() => _LoginState();
}
class _LoginState extends State<Login> {

TextEditingController emailCotroller =TextEditingController();
TextEditingController passwordController = TextEditingController();

void login(String email , password) async{

  try{
     Response response = await post(
      Uri.parse("https://reqres.in/api/register"),
      body :{
        "email" : email,
        "password": password
      }
     );
         if (response.statusCode == 200) {
             var data = jsonDecode(response.body.toString());
          print("Account Created ");
         }
         else{
          print("failed");
         }
  }
  catch(e){
    print(e.toString());

  }
}
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: Column(
          children: [
             SizedBox(
              height: 50,
            ),
            TextFormField(
              controller: emailCotroller,
              decoration: InputDecoration(
                hintText: 'Enter your Email'
              ),
            ),
            SizedBox(
              height: 20,
            ),
              TextFormField(
              controller: passwordController,
              decoration: InputDecoration(
                hintText: 'password'
              ),
            ),
              SizedBox(
              height: 40,
            ),
            GestureDetector(
              onTap: () {
                login(emailCotroller.text.toString(),passwordController.text.toString());
               // print('object');
              },
              child: Container(
                height: 30,
                decoration: BoxDecoration(
                  color: Colors.blue,
                ),
                child: Center(
                  child: Text('SingUp'),
                ),
              ),
            ),
            SizedBox(
              height: 20,
            ),
            Container(
              height: 10,
            
            )
          ],
        ),
      ),
    
    );
  }
}


