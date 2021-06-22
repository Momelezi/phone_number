# phone_number
#convert phone number from string into an interger


# 2 Converting phone numbers
# 2.1 From string to int

def number_string_to_int(num_string):
		digits = "0123456789"
		final_num = ""
		for char in num_string:
		    if char in digits:		
				    final_num += char
		return int(final_num)

# 2.2 From int to string

def number_to_string(number):
    num_string = str(number) 	
    output_string = "0" + num_string[0:2] + " " + num_string[2:5] + " " + num_string[5:9]
    return output_string

# 3 Managing phone numbers
# 3.1 Adding a phone number into the phonebook

def add_phonebook_entry(name_string, number_string): 
                global names, numbers 
                clean_number = number_string_to_int(number_string)
                found = False
                for index in range(len(numbers)):
	                   if numbers[index] == clean_number:
	                                      found = True
	                                      break
                if found:
	                   print("Error: number already in the phonebook, associated with name " + names[index])
                else:
	                names.append(name_string)
	                numbers.append(clean_number)
                return None


# 3.2 Querying the phonebook for a phone number

def query_by_name(name_string):
                global names, numbers
                for i in range(len(names)):
	                   if names[i].lower() == name_string.lower():
	                                     print(number_to_string(numbers[i]))
	                                     return None
                print("Contact not found")
                return None


# 3.3 Printing the whole phonebook

def print_book():
                global names, numbers
                for i in range(len(names)):
	                         print(names[i], ":", number_to_string(numbers[i]))
                return None

# 3.4 Modifying a phone number

def update_number(old, new):
                global numbers
                old_num_clean = number_string_to_int(old)
                found = False
                for i in range(len(numbers)):
	                 if numbers[i] == old_num_clean:
	                             found = True
	                             numbers[i] = number_string_to_int(new)
	                             break
                if not found: 
	                 print("Warning! Was unable to update number, as old one was not present in the phonebook.")
                return None


# 3.5 Deleting a phone number from the phonebook

def delete_num(num_to_delete):
                global names, numbers
                num_clean = number_string_to_int(num_to_delete)
                found = False
                for i in range(len(numbers)): 
	                 if numbers[i] == num_clean:
	                            found = True
	                            if i == len(numbers) - 1:
		                               numbers.pop()	
		                               names.pop()		
	                            else:
		                               numbers[i] = numbers.pop()
		                               names[i] = names.pop()
                if not found:
	                 print("Warning! Was unable to delete this number, as it was not present in the phonebook.")
                return None

# 4 Interactive loop


names = [ "Viwe", "Siseko", "Vuyo", "Esethu" ]
numbers = [ 731289950, 745043136, 847084847, 825351438 ]
while True:
    print("")
    print("Please enter a command number:")
    print("p -> print phonebook contents")
    print("a -> add a new entry")
    print("u -> update an entry")
    print("s -> search for a name")
    print("d -> delete an entry")
    print("e -> exit this program")
    print("")
    command = input()
    if command == "p":
	           print_book()
    elif command == "n":
	           name_to_add = input("Please enter the name of the new contact: ")
	           num_to_add = input("Please enter " + name_to_add + "'s phone number: ")
	           add_phonebook_entry(name_to_add, num_to_add)
    elif command == "u":
	           old_num = input("Please enter the contact's old phone number: ")
	           new_num = input("Please enter the new number for the same contact: ")
	           update_number(old_num, new_num)
    elif command == "s":
	           name_to_lookup = input("Please enter the name of the contact to query: ")
	           query_by_name(name_to_lookup)
    elif command == "d":
	           num_to_delete = input("Please enter the phone number to delete: ")
	           delete_num(num_to_delete)
    elif command == "q":
	           break
    else:
	           print("Unrecognized command, try again!")



