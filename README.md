# new-print
package Elena;

import java.time.Instant;

public class User {
	
	enum Status {
		ACTIVE, INACTIVE, BLOCKED, NEW
	}
	
	private String firstName, lastName, eMail;
	private int age, id;
	private Instant time;
	private Status status;

	public User(int id, String firstName, String lastName, String eMail,
			int age, Instant time, Status status) {
		this.firstName = firstName;
		this.lastName = lastName;
		this.eMail = eMail;
		this.age = age;
		this.id = id;
		this.time = time;
		this.status = status;
	}

	public void setId(int id) {
		this.id = id;
	}

	public int getId() {
		return this.id;
	}

	public void setFirstName(String firstName) {
		this.firstName = firstName;
	}

	public String getFirstName() {
		return this.firstName;
	}

	public void setLastName(String lastName) {
		this.lastName = lastName;
	}

	public String getLastName() {
		return this.lastName;
	}

	public void setAge(int age) {
		if (age >= 0)
			this.age = age;
	}

	public int getAge() {
		return this.age;
	}

	public void setEMail(String eMail) {
		this.eMail = eMail;
	}

	public String getEMail() {
		return this.eMail;
	}

	public void setStatus(Status status) {
		this.status = status;
	}

	public Status getStatus() {
		return this.status;
	}

	public void setTime(Instant time) {
		this.time = time;
	}

	public Instant getTime() {
		return this.time;
	}

	@Override
	public String toString() {
		return "User" + id + " [First name: " + firstName + "; Last name: " + lastName + "; Age: " + age + "; e-Mail: "
				+ eMail + "; Status: " + status.name() + "; Timestamp " + time + "]";

	}
	
}

package Elena;


import java.time.Instant;
import java.time.temporal.ChronoUnit;
import java.util.ArrayList;
import java.util.List;

import Elena.User.Status;

public class Application {
	
	public static void main(String[] args) {
		
		
		User user1 = new User(1, "E", "H", "eh@gmail.com", 30, Instant.now().minus(2, ChronoUnit.DAYS), Status.NEW);
		User user2 = new User(2, "V", "H", "vh@gmail.com", 25, Instant.now().minus(32, ChronoUnit.DAYS), Status.INACTIVE);
		User user3 = new User(3, "R", "M", "rm@gmail.com", 29, Instant.now(), Status.NEW);
		User user4 = new User(4, "I", "C", "ic@gmail.com", 32, Instant.now(), Status.NEW);
		User user5 = new User(5, "A", "C", "ac@gmail.com", 18, Instant.now(), Status.NEW);
		User user6 = new User(6, "A", "B", "ab@gmail.com", 24, Instant.now().minus(3, ChronoUnit.DAYS), Status.NEW);
		User user7 = new User(7, "I", "R", "ir@gmail.com", 26, Instant.now(), Status.NEW);
		User user8 = new User(8, "R", "M", "rm@gmail.com", 21, Instant.now().minus(60, ChronoUnit.DAYS), Status.INACTIVE);
		User user9 = new User(9, "C", "H", "ch@gmail.com", 29, Instant.now().minus(7, ChronoUnit.DAYS), Status.ACTIVE);
		User user10 = new User(10, "A", "C", "ac@gmail.com", 31, Instant.now(), Status.NEW);
		
		List<User> users = new ArrayList<>();
			
		users.add(user1);
		users.add(user2);
		users.add(user3);
		users.add(user4);
		users.add(user5);
		users.add(user6);
		users.add(user7);
		users.add(user8);
		users.add(user9);
		users.add(user10);
		
		
		printUsers(users);
		System.out.println("--------");
		modifyUserStatus(users, Status.NEW, 1, Status.ACTIVE);
		printUsers(users);
		System.out.println("--------");
		modifyUserStatus(users, Status.INACTIVE, 30, Status.BLOCKED);
		printUsers(users);
			}
	
	private static void modifyUserStatus(List<User> users, Status currentStatus, int createdDaysAgo, Status changeStatusTo) {
		for (int i = 0; i < users.size(); i++) {
			User currentUser = users.get(i); 
			if (currentUser.getStatus().equals(currentStatus) && 
					currentUser.getTime().isBefore(Instant.now().minus(createdDaysAgo, ChronoUnit.DAYS))) {
				currentUser.setStatus(changeStatusTo);
			}
		}
	}
	
	private static void printUsers(List<User> users) {
		for (int i = 0; i < users.size(); i++) {
			printUser(users.get(i));
		}
	}
	
	private static void printUser(User user) {
		System.out.println(user);
	}

}
	
	
