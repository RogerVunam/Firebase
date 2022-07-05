# Firebase

# Step1 : Link Library and Step by Step
```
https://firebase.google.com/docs/android/setup?hl=en&authuser=0
```

# Step2 : Làm Step by step theo Option1
![1](https://user-images.githubusercontent.com/108450566/177335966-4a57344f-9888-4dcd-924c-2e2433884dd6.jpg)


# Step3 : Cách post 1 request tạo 1 table lên Firebase RealtimeDatabase
```
val database = Firebase.database("https://practice-e2276-default-rtdb.asia-southeast1.firebasedatabase.app/").getReference("Users")
```
Cái này là để truy xuất vào database để tham chiếu đến Table Users


# Step4 : Tạo Model có những thuộc tính cần tạo
```

data class User constructor(
    ///basic info
    var email: String,
    var fullName: String,
    var topTopID: String,
    var password: String,
    var follower: Int = 0,
    var following: Int = 0,
    var hearts: Int = 0,
    var favorites: Int = 0,
    var imgUrl: String,
    ///update
    var videoID: String,
    var phone: String,
    var profileUrl: String,
)
```
```

data class Comment(
    val idComment: String,
    val message: String,
    val fullName: String,
    val createAt: String,
    val updateAt: String,
    val comments: Double,
    val hearts: Double
)
```
# Tạo user 
```
val user = User(email, "", topTopID,password,0,0,0,0,"","","","")
```
![2](https://user-images.githubusercontent.com/108450566/177336794-f0f9cee0-74bf-4313-97c9-8d3802bf98a0.jpg)
# So sánh với data đã post 
![1](https://user-images.githubusercontent.com/108450566/177337402-4eef15f6-75ae-411d-8756-4d20a91cfc3c.jpg)


# Step5 : Tạo Primarykey theo 1 trường mình nhập từ màn hình ( Sử dụng database.push().key)
```
val topTopID = binding.edtTopTopID.text.toString().trim()
database.push().key == topTopID
```
# Có thể tạo biến id = database.push().key rồi gán == với trường mình vừa nhập
```
val topTopID = binding.edtTopTopID.text.toString().trim()
val identifier = database.push().key
identifier == topTopID
```

# Step6 : Truy cập vào con của nhánh cha để setValue bằng câu lệnh này
```
database.child(identifier).setValue(user)
```
Sau đó theo dõi thành công hay thất bại bằng cách truy xuất vào

.addOnCompleteListener

.addOnFailureListener
```
database.child(user.topTopID).setValue(user)
            .addOnCompleteListener {
                Toast.makeText(requireContext(),"Insert Succesfully",Toast.LENGTH_SHORT).show()
                findNavController().navigate(R.id.action_signUpFM_to_signInFM)
            }
            .addOnFailureListener { error->
                Toast.makeText(requireContext(),"Failure ${error.message}",Toast.LENGTH_SHORT).show()
            }
```
# hoặc
```
database.child(identifier).setValue(user)
            .addOnCompleteListener {
                Toast.makeText(requireContext(),"Insert Succesfully",Toast.LENGTH_SHORT).show()
                findNavController().navigate(R.id.action_signUpFM_to_signInFM)
            }
            .addOnFailureListener { error->
                Toast.makeText(requireContext(),"Failure ${error.message}",Toast.LENGTH_SHORT).show()
            }
```
# Lưu ý là child() là đang vô lớp con 



