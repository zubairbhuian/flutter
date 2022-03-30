
## Form Validation with *RegExp*
``` dart
import 'package:flutter/material.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(primarySwatch: Colors.green),
      home: Scaffold(
        appBar: AppBar(title: const Text("User Informatoin")),
        body:const UserForm(),
      ),
    );
  }
}

class UserForm extends StatefulWidget {
  const UserForm({Key? key}) : super(key: key);

  @override
  State<UserForm> createState() => _UserFormState();
}

class _UserFormState extends State<UserForm> {
  bool isPasswardShow = true;
  final GlobalKey<FormState> formKey = GlobalKey<FormState>();
  // textController
  final TextEditingController _emailController = TextEditingController();
  final TextEditingController _passController = TextEditingController();
  @override
  Widget build(BuildContext context) {
    return Form(
      key: formKey,
      // autovalidateMode: AutovalidateMode.always,
      child: ListView(
        padding: const EdgeInsets.only(top: 100, left: 20, right: 20),
        children: [
          TextFormField(
            keyboardType: TextInputType.emailAddress,
            controller: _emailController,
            decoration: const InputDecoration(
                border: OutlineInputBorder(), label: Text("Email")),
            validator: (value) {
              if (value!.isEmpty ||
                  !RegExp(r'^[\w-\.]+@([\w-]+\.)+[\w]{2,4}').hasMatch(value)) {
                return "Enter Valide Email";
              } else {
                return null;
              }
            },
          ),
          const SizedBox(height: 20),
          TextFormField(
            controller: _passController,
            obscureText: isPasswardShow,
            keyboardType: TextInputType.number,
            decoration: InputDecoration(
                border: const OutlineInputBorder(),
                label: const Text("Password"),
                suffix: InkWell(
                  child: isPasswardShow == true
                      ? const Icon(Icons.visibility)
                      : const Icon(Icons.visibility_off),
                  onTap: () {
                    setState(() {
                      isPasswardShow = !isPasswardShow;
                    });
                  },
                )),
            validator: (value) {
              if (value!.isEmpty || !RegExp(r'^[w-]').hasMatch(value)) {
                return "Enter Valid Password";
              } else {
                return null;
              }
            },
          ),
          const SizedBox(height: 20),
          ElevatedButton(
              onPressed: () {
                if (formKey.currentState!.validate()) {
                  // Process data.
                }
              },
              child: const Text("Submit"))
        ],
      ),
    );
  }
}


```