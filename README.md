  #include <iostream>
   #include <cstring>
   using namespace std;
   class String
   {
           private:
           char* str;
           size_t length;
  
          public:
           String()
          {
                  str = new char[1];
                  str[0] = '\0';
                   length = 0;
            }
 
              String(const char* s)
           {
                   length = std::strlen(s);
                   str = new char[length + 1];
                    std::strcpy(str, s);
          }
 
          String(const String& other)
          {
                  length = other.length;
                  str = new char[length + 1];
                  std::strcpy(str, other.str);
          }
 
          ~String()
          {
                  delete[] str;
          }
 
      String& operator=(const String& other)
          {
         if (this != &other)
                 {
                 delete[] str;
                         length = other.length;
                          str = new char[length + 1];
                      std::strcpy(str, other.str);
                  }
                  return *this;
           }
 
              const char* c_str() const
          {
                  return str;
          }
 
            size_t getLength() const
          {
                  return length;
          }
 
      void strcpy(const String& other)
          {
                  delete[] str;
                  length = other.length;
                  str = new char[length + 1];
                  std::strcpy(str, other.str);
          }
 
      void strncpy(const String& other, size_t n)
         {
                  length = (n < other.length) ? n : other.length;
                  str = new char[length + 1];
                  std::strncpy(str, other.str, n);
                   str[length] = '\0';
          }
 
      int strcmp(const String& other) const
           {
                  return std::strcmp(str, other.str);
  }

int strncmp(const String& other, size_t n) const
           {
                  return std::strncmp(str, other.str, n);
          }
 
      void strcat(const String& other)
         {  
          char* newStr = new char[length + other.length + 1];
                 std::strcpy(newStr, str);
                  std::strcat(newStr, other.str);
                  delete[] str;
                  str = newStr;
                   length += other.length;
      }
       void strncat(const String& other, size_t n)
          {
                  size_t copyLength = (n < other.length) ? n : other.lengt    h;
                  char* newStr = new char[length + copyLength + 1];
                  std::strcpy(newStr, str);
                 std::strncpy(newStr + length, other.str, copyLength);
                 newStr[length + copyLength] = '\0';

                 delete[] str;
                 str = newStr;
                 length += copyLength;
        }

     void strrev()
         {
                 size_t left = 0, right = length - 1;
                while (left < right)
                 {
                    std::swap(str[left], str[right]);
                    left++;
                   right--;
                  }
         }

   void strupper()
 {
                 for (size_t i = 0; i < length; ++i)
                  {
                     str[i] = std::toupper(str[i]);
                  }
     }
     void strlower()
         {
                 for (size_t i = 0; i < length; ++i)
                  {
                         str[i] = std::tolower(str[i]);                  }
        }

     const char* strchr(char c) const
         {
                 return std::strchr(str, c);
          }

          const char* strrchr(char c) const
                 {
                  return std::strrchr(str, c);
                 }

     const char* strstr(const String& other) const
         {
                 return std::strstr(str, other.str);
         }

     size_t strlen() const
          {
                 return length;
          }

         friend std::ostream& operator<<(std::ostream& os, const String&     s)
          {
                os << s.str;
                return os;
         }

         friend std::istream& operator>>(std::istream& is, String& s)
         {
                 char buffer[1000];
                 is >> buffer;
               s = String(buffer);
         return is;
}
};
void displayMenu()
  {
std::cout << "\n |\033[33m *****CHOOSE AN OPERATION TO PERFORM THE T    ASK*****\033[0m | \n";
     std::cout << "1. Concatenate two strings\n";
     std::cout << "2. Compare two strings\n";
     std::cout << "3. Copy a string\n";
     std::cout << "4. Reverse the string\n";
     std::cout << "5. Convert to uppercase\n";
     std::cout << "6. Convert to lowercase\n";
    std::cout << "7. Find a character in the string\n";
     std::cout << "8. Find the last occurrence of a character\n";
     std::cout << "9. Find a substring\n";
     std::cout << "10. Display the string\n";
     std::cout << "11. Exit\n";
     std::cout << "\n|\033[33m******Enter your choice:******\033[033[0m|\    n ";
}
void performOperations()
 {
     String str1, str2;

   std::cout << "Enter the first string: ";
   std::cin >> str1;
    int choice;
    bool running = true;
  while (running)
          {
           displayMenu();
            std::cin >> choice;

         switch (choice)
          {
             case 1:
                 {
                         std::cout << "Enter the second string: ";
                         std::cin >> str2;
                         str1.strcat(str2);
                          std::cout << "Concatenated string: " << str1 <<     std::endl;
                   break;
             }

             case 2:
                 {
                          std::cout << "Enter the second string: ";
                          std::cin >> str2;
                         int result = str1.strcmp(str2);

                    if (result == 0)                         {
                         std::cout << "The strings are equal.\n";
                 }
                 else if (result > 0)
                 {
                     std::cout << "The first string is greater than the s    econd string.\n";
                 } else
                 {
                  std::cout << "The first string is less than the seco    nd string.\n";
                 }
                 break;
             }
             case 3:
          {
                 std::cout << "Enter the string to copy: ";
                 std::cin >> str2;
                 str1.strcpy(str2);
                 std::cout << "Copied string: " << str1 << std::endl;
                break;     
                 }
             case 4:
         {
                 str1.strrev();
                 std::cout << "Reversed string: " << str1 << std::endl;
                 break;
}
             case 5:
{
                        str1.strupper();
                         std::cout << "Uppercase string: " << str1 << std    ::endl;
                 break;
                 }

            case 6:
         {
                 str1.strlower();
                 std::cout << "Lowercase string: " << str1 << std::endl;
                 break;
             }

             case 7:
         {
                 char c;
                 std::cout << "Enter character to find: ";
                 std::cin >> c;
                 const char* result = str1.strchr(c);
                 if (result)
         {
         std::cout << "Character '" << c << "' found at posit    ion: " << (result - str1.c_str()) << std::endl;
         } else
          {
                     std::cout << "Character not found.\n";
              }
                 break;
            }

            case 8:
  {
                 char c;
                 std::cout << "Enter character to find: ";
                 std::cin >> c;
                 const char* result = str1.strrchr(c);
                 if (result)
         {
                     std::cout << "Last occurrence of character '" << c <    < "' at position: " << (result - str1.c_str()) << std::endl;
                 } else
          {
                     std::cout << "Character not found.\n";
                 }
                 break;
             }
             case 9:
          {
                 std::cout << "Enter the substring to find: ";
                 std::cin >> str2;
  const char* result = str1.strstr(str2);
                 if (result)
         {
                     std::cout << "Substring found at position: " << (res    ult - str1.c_str()) << std::endl;
                }
                 else
                  {
                   std::cout << "Substring not found.\n";
                 }
                 break;
             }
             case 10:
          {
                 std::cout << "The current string is: " << str1 << std::e    ndl;
                 break;
             }
             case 11:
         {
                 running = false;
                 break;
          }
             default:
         {
                 std::cout << "Invalid choice. Please try again.\n";
                 break;
             }
         }
     }
 }
int main()
 {
     performOperations();
return 0;
 }
