# PERTEMUAN 7: JAVASCRIPT ASYNC PROGRAMMING - Orkestrasi Waktu Digital ⏰

## ⏰ **Filosofi Async: Seni Mengelola Waktu dalam Programming**

Asynchronous programming adalah seperti **konduktor orkestra digital** yang mengatur berbagai musicians (processes) bermain pada timing yang tepat tanpa membuat audience (user) menunggu. Dalam dunia web yang real-time, kemampuan mengelola multiple tasks secara concurrent adalah kunci aplikasi yang responsif dan modern.

### **Analogi: Async sebagai Restoran dengan Multiple Orders**

```
Synchronous: Satu chef, satu order, tunggu selesai, baru order berikutnya
Asynchronous: Multiple chefs, multiple orders, parallel processing, serve when ready
```

## 🔄 **Evolution of Async - Perjalanan Waktu JavaScript**

### **1. Era Callbacks - Foundation of Async**

**Analogi: Callbacks seperti "Call Me When Ready"**

```javascript
// Callback Pattern - The Foundation
class CallbackDemo {
  // Simulate network request dengan callback
  static fetchUserData(userId, callback) {
    console.log(`🔍 Mencari data user ${userId}...`);

    // Simulate network delay
    setTimeout(() => {
      const userData = {
        id: userId,
        name: "Nazriel Rahman Al'afath",
        email: "nazriel@email.com",
        major: "Teknik Informatika",
        joinedAt: new Date().toISOString(),
      };

      // Simulate possible error
      const success = Math.random() > 0.2; // 80% success rate

      if (success) {
        console.log(`✅ Data user ${userId} berhasil dimuat`);
        callback(null, userData); // null = no error
      } else {
        console.log(`❌ Gagal memuat data user ${userId}`);
        callback(new Error("Network error"), null);
      }
    }, 1000 + Math.random() * 2000); // 1-3 seconds delay
  }

  // Callback hell example - The Problem
  static demonstrateCallbackHell(userId) {
    console.log("🌀 Demonstrasi Callback Hell...");

    this.fetchUserData(userId, (err1, user) => {
      if (err1) {
        console.error("❌ Error getting user:", err1.message);
        return;
      }

      console.log("👤 User data:", user);

      // Fetch user's courses
      this.fetchUserCourses(user.id, (err2, courses) => {
        if (err2) {
          console.error("❌ Error getting courses:", err2.message);
          return;
        }

        console.log("📚 User courses:", courses);

        // Fetch course details for each course
        const courseDetails = [];
        let completedRequests = 0;

        courses.forEach((course, index) => {
          this.fetchCourseDetails(course.id, (err3, details) => {
            if (err3) {
              console.error(
                `❌ Error getting course ${course.id}:`,
                err3.message
              );
              return;
            }

            courseDetails[index] = details;
            completedRequests++;

            // When all course details are loaded
            if (completedRequests === courses.length) {
              console.log("📖 Course details:", courseDetails);

              // Calculate user statistics
              this.calculateUserStats(user, courseDetails, (err4, stats) => {
                if (err4) {
                  console.error("❌ Error calculating stats:", err4.message);
                  return;
                }

                console.log("📊 User statistics:", stats);
                console.log("🎯 Callback Hell completed (but what a mess!)");
              });
            }
          });
        });
      });
    });
  }

  static fetchUserCourses(userId, callback) {
    setTimeout(() => {
      const courses = [
        { id: "WEB001", name: "Web Programming" },
        { id: "DB001", name: "Database Systems" },
        { id: "SE001", name: "Software Engineering" },
      ];
      callback(null, courses);
    }, 800);
  }

  static fetchCourseDetails(courseId, callback) {
    setTimeout(() => {
      const details = {
        id: courseId,
        credits: 3,
        semester: 5,
        grade: "A",
        instructor: "Dr. Ahmad Subhan",
      };
      callback(null, details);
    }, 500);
  }

  static calculateUserStats(user, courseDetails, callback) {
    setTimeout(() => {
      const totalCredits = courseDetails.reduce(
        (sum, course) => sum + course.credits,
        0
      );
      const avgGrade = 3.85; // Simplified calculation

      const stats = {
        totalCourses: courseDetails.length,
        totalCredits,
        averageGrade: avgGrade,
        status: avgGrade >= 3.5 ? "Excellent" : "Good",
      };

      callback(null, stats);
    }, 300);
  }
}

// Usage - Callback Hell in Action
console.log("🔥 Starting Callback Hell Demo...");
CallbackDemo.demonstrateCallbackHell("20230001");
```

### **2. Era Promises - Chainable Future**

**Analogi: Promise seperti "Janji yang Bisa Dipercaya"**

```javascript
// Promise Pattern - Better Error Handling & Chaining
class PromiseDemo {
  // Convert callback to Promise
  static fetchUserData(userId) {
    console.log(`🔍 [Promise] Mencari data user ${userId}...`);

    return new Promise((resolve, reject) => {
      setTimeout(() => {
        const userData = {
          id: userId,
          name: "Nazriel Rahman Al'afath",
          email: "nazriel@email.com",
          major: "Teknik Informatika",
          enrolledCourses: ["WEB001", "DB001", "SE001"],
          gpa: 3.85,
          joinedAt: new Date().toISOString(),
        };

        const success = Math.random() > 0.2;

        if (success) {
          console.log(`✅ [Promise] Data user ${userId} berhasil dimuat`);
          resolve(userData);
        } else {
          console.log(`❌ [Promise] Gagal memuat data user ${userId}`);
          reject(new Error("Network error while fetching user data"));
        }
      }, 1000 + Math.random() * 1000);
    });
  }

  static fetchUserCourses(userId) {
    console.log(`📚 [Promise] Mengambil courses untuk user ${userId}...`);

    return new Promise((resolve, reject) => {
      setTimeout(() => {
        const courses = [
          {
            id: "WEB001",
            name: "Web Programming",
            instructor: "Prof. Budi Raharjo",
            credits: 3,
            schedule: "Monday 08:00-10:00",
          },
          {
            id: "DB001",
            name: "Database Systems",
            instructor: "Dr. Siti Aminah",
            credits: 3,
            schedule: "Wednesday 10:00-12:00",
          },
          {
            id: "SE001",
            name: "Software Engineering",
            instructor: "Dr. Ahmad Subhan",
            credits: 3,
            schedule: "Friday 13:00-15:00",
          },
        ];

        console.log(
          `✅ [Promise] Courses untuk user ${userId} berhasil dimuat`
        );
        resolve(courses);
      }, 800);
    });
  }

  static fetchCourseGrades(userId, courseIds) {
    console.log(
      `📊 [Promise] Mengambil nilai untuk ${courseIds.length} courses...`
    );

    return new Promise((resolve) => {
      setTimeout(() => {
        const grades = courseIds.map((courseId) => ({
          courseId,
          grade: "A",
          score: 85 + Math.random() * 15, // 85-100
          completed: true,
          semester: 5,
        }));

        console.log(`✅ [Promise] Grades berhasil dimuat`);
        resolve(grades);
      }, 600);
    });
  }

  static calculateSemesterStats(user, courses, grades) {
    console.log(`🧮 [Promise] Menghitung statistik semester...`);

    return new Promise((resolve) => {
      setTimeout(() => {
        const totalCredits = courses.reduce(
          (sum, course) => sum + course.credits,
          0
        );
        const totalScore = grades.reduce((sum, grade) => sum + grade.score, 0);
        const averageScore = totalScore / grades.length;

        let letterGrade = "F";
        if (averageScore >= 85) letterGrade = "A";
        else if (averageScore >= 80) letterGrade = "B+";
        else if (averageScore >= 75) letterGrade = "B";
        else if (averageScore >= 70) letterGrade = "C+";
        else if (averageScore >= 65) letterGrade = "C";

        const stats = {
          studentName: user.name,
          totalCourses: courses.length,
          totalCredits,
          averageScore: parseFloat(averageScore.toFixed(2)),
          letterGrade,
          semesterGPA: parseFloat((averageScore / 25).toFixed(2)), // Convert to 4.0 scale
          status:
            averageScore >= 80
              ? "Excellent"
              : averageScore >= 70
              ? "Good"
              : "Needs Improvement",
          completionDate: new Date().toISOString(),
        };

        console.log(`✅ [Promise] Statistik semester berhasil dihitung`);
        resolve(stats);
      }, 400);
    });
  }

  // Promise Chain - Much cleaner than callbacks
  static demonstratePromiseChain(userId) {
    console.log("⛓️ Demonstrasi Promise Chain...");

    let userData;
    let coursesData;
    let gradesData;

    return this.fetchUserData(userId)
      .then((user) => {
        userData = user;
        console.log("👤 User data loaded:", user.name);
        return this.fetchUserCourses(user.id);
      })
      .then((courses) => {
        coursesData = courses;
        console.log(`📚 ${courses.length} courses loaded`);
        return this.fetchCourseGrades(
          userData.id,
          courses.map((c) => c.id)
        );
      })
      .then((grades) => {
        gradesData = grades;
        console.log(`📊 Grades loaded for ${grades.length} courses`);
        return this.calculateSemesterStats(userData, coursesData, gradesData);
      })
      .then((stats) => {
        console.log("🎯 Final statistics:", stats);
        console.log("✨ Promise Chain completed successfully!");
        return {
          user: userData,
          courses: coursesData,
          grades: gradesData,
          stats: stats,
        };
      })
      .catch((error) => {
        console.error("💥 Error in Promise Chain:", error.message);
        throw error;
      });
  }

  // Promise.all - Parallel execution
  static demonstratePromiseAll(userIds) {
    console.log("🚀 Demonstrasi Promise.all (Parallel Execution)...");

    const userPromises = userIds.map((userId) => this.fetchUserData(userId));

    return Promise.all(userPromises)
      .then((users) => {
        console.log(
          `✅ Semua ${users.length} users berhasil dimuat secara parallel`
        );

        // Process all users data
        const summary = {
          totalUsers: users.length,
          majors: [...new Set(users.map((u) => u.major))],
          averageGPA: users.reduce((sum, u) => sum + u.gpa, 0) / users.length,
          userNames: users.map((u) => u.name),
        };

        console.log("📊 Users Summary:", summary);
        return { users, summary };
      })
      .catch((error) => {
        console.error("💥 Error loading users:", error.message);
        throw error;
      });
  }

  // Promise.allSettled - Handle partial failures
  static demonstratePromiseAllSettled(userIds) {
    console.log("🛡️ Demonstrasi Promise.allSettled (Fault Tolerant)...");

    const userPromises = userIds.map((userId) => this.fetchUserData(userId));

    return Promise.allSettled(userPromises).then((results) => {
      const successful = results.filter((r) => r.status === "fulfilled");
      const failed = results.filter((r) => r.status === "rejected");

      console.log(`✅ Berhasil: ${successful.length} users`);
      console.log(`❌ Gagal: ${failed.length} users`);

      const users = successful.map((r) => r.value);

      return {
        successful: users,
        failed: failed.map((r) => r.reason.message),
        summary: {
          successRate:
            ((successful.length / results.length) * 100).toFixed(1) + "%",
          totalAttempts: results.length,
        },
      };
    });
  }
}

// Usage Examples
console.log("🔗 Starting Promise Chain Demo...");
PromiseDemo.demonstratePromiseChain("20230001").then((result) => {
  console.log("🎊 Promise Chain Result:", result.stats);
});

// Parallel execution
console.log("\n🚀 Starting Promise.all Demo...");
PromiseDemo.demonstratePromiseAll(["20230001", "20230002", "20230003"]).then(
  (result) => {
    console.log("🎊 Promise.all Result:", result.summary);
  }
);

// Fault tolerant execution
console.log("\n🛡️ Starting Promise.allSettled Demo...");
PromiseDemo.demonstratePromiseAllSettled([
  "20230001",
  "invalid",
  "20230003",
]).then((result) => {
  console.log("🎊 Promise.allSettled Result:", result.summary);
});
```

### **3. Era Async/Await - Synchronous-looking Async**

**Analogi: Async/Await seperti "Magic that Looks Normal"**

```javascript
// Async/Await Pattern - The Modern Way
class AsyncAwaitDemo {
  // Same functions as Promise demo, but used with async/await
  static fetchUserData(userId) {
    return PromiseDemo.fetchUserData(userId);
  }

  static fetchUserCourses(userId) {
    return PromiseDemo.fetchUserCourses(userId);
  }

  static fetchCourseGrades(userId, courseIds) {
    return PromiseDemo.fetchCourseGrades(userId, courseIds);
  }

  static calculateSemesterStats(user, courses, grades) {
    return PromiseDemo.calculateSemesterStats(user, courses, grades);
  }

  // Async/Await - Clean and readable
  static async demonstrateAsyncAwait(userId) {
    console.log("✨ Demonstrasi Async/Await...");

    try {
      // Sequential execution (wait for each step)
      console.log("📥 Step 1: Loading user data...");
      const user = await this.fetchUserData(userId);
      console.log("👤 User loaded:", user.name);

      console.log("📥 Step 2: Loading user courses...");
      const courses = await this.fetchUserCourses(user.id);
      console.log(`📚 ${courses.length} courses loaded`);

      console.log("📥 Step 3: Loading course grades...");
      const grades = await this.fetchCourseGrades(
        user.id,
        courses.map((c) => c.id)
      );
      console.log(`📊 Grades loaded for ${grades.length} courses`);

      console.log("📥 Step 4: Calculating statistics...");
      const stats = await this.calculateSemesterStats(user, courses, grades);
      console.log("🎯 Statistics calculated");

      const result = {
        user,
        courses,
        grades,
        stats,
        processingTime: new Date().toISOString(),
      };

      console.log("✅ Async/Await completed successfully!");
      console.log("📋 Final Result:", stats);

      return result;
    } catch (error) {
      console.error("💥 Error in Async/Await:", error.message);
      throw error;
    }
  }

  // Parallel execution with async/await
  static async demonstrateParallelExecution(userIds) {
    console.log("🚀 Demonstrasi Parallel Execution dengan Async/Await...");

    try {
      // Start all requests simultaneously
      console.log(`🔄 Starting ${userIds.length} parallel user requests...`);
      const userPromises = userIds.map((userId) => this.fetchUserData(userId));

      // Wait for all to complete
      const users = await Promise.all(userPromises);
      console.log(`✅ All ${users.length} users loaded in parallel`);

      // Process each user's courses in parallel
      console.log("🔄 Loading courses for all users in parallel...");
      const coursePromises = users.map((user) =>
        this.fetchUserCourses(user.id)
      );
      const coursesArrays = await Promise.all(coursePromises);

      // Combine results
      const results = users.map((user, index) => ({
        user,
        courses: coursesArrays[index],
        coursesCount: coursesArrays[index].length,
      }));

      const summary = {
        totalUsers: users.length,
        totalCourses: coursesArrays.flat().length,
        averageCoursesPerUser:
          coursesArrays.reduce((sum, courses) => sum + courses.length, 0) /
          users.length,
        majors: [...new Set(users.map((u) => u.major))],
        processedAt: new Date().toISOString(),
      };

      console.log("📊 Parallel Execution Summary:", summary);
      return { results, summary };
    } catch (error) {
      console.error("💥 Error in parallel execution:", error.message);
      throw error;
    }
  }

  // Error handling with try/catch in different levels
  static async demonstrateErrorHandling(userIds) {
    console.log("🛡️ Demonstrasi Error Handling dengan Async/Await...");

    const results = [];
    const errors = [];

    for (const userId of userIds) {
      try {
        console.log(`🔄 Processing user ${userId}...`);

        const user = await this.fetchUserData(userId);
        console.log(`✅ User ${userId} loaded successfully`);

        try {
          const courses = await this.fetchUserCourses(user.id);
          console.log(`✅ Courses for ${userId} loaded successfully`);

          results.push({
            user,
            courses,
            status: "success",
          });
        } catch (courseError) {
          console.warn(
            `⚠️ Failed to load courses for ${userId}: ${courseError.message}`
          );

          // Partial success - user loaded but courses failed
          results.push({
            user,
            courses: [],
            status: "partial",
            error: courseError.message,
          });
        }
      } catch (userError) {
        console.error(`❌ Failed to load user ${userId}: ${userError.message}`);

        errors.push({
          userId,
          error: userError.message,
          timestamp: new Date().toISOString(),
        });
      }
    }

    const summary = {
      total: userIds.length,
      successful: results.filter((r) => r.status === "success").length,
      partial: results.filter((r) => r.status === "partial").length,
      failed: errors.length,
      successRate: ((results.length / userIds.length) * 100).toFixed(1) + "%",
    };

    console.log("📊 Error Handling Summary:", summary);

    return {
      results,
      errors,
      summary,
    };
  }

  // Advanced: Concurrent with limit (rate limiting)
  static async demonstrateConcurrentWithLimit(userIds, limit = 2) {
    console.log(
      `🎛️ Demonstrasi Concurrent Execution dengan Limit (${limit} concurrent)...`
    );

    const results = [];

    // Process in batches
    for (let i = 0; i < userIds.length; i += limit) {
      const batch = userIds.slice(i, i + limit);
      console.log(
        `🔄 Processing batch ${Math.floor(i / limit) + 1}: [${batch.join(
          ", "
        )}]`
      );

      const batchPromises = batch.map(async (userId) => {
        try {
          const user = await this.fetchUserData(userId);
          const courses = await this.fetchUserCourses(user.id);
          return { userId, user, courses, status: "success" };
        } catch (error) {
          return { userId, error: error.message, status: "failed" };
        }
      });

      const batchResults = await Promise.all(batchPromises);
      results.push(...batchResults);

      console.log(`✅ Batch ${Math.floor(i / limit) + 1} completed`);

      // Optional: Add delay between batches
      if (i + limit < userIds.length) {
        console.log("⏳ Waiting before next batch...");
        await new Promise((resolve) => setTimeout(resolve, 500));
      }
    }

    const summary = {
      totalProcessed: results.length,
      successful: results.filter((r) => r.status === "success").length,
      failed: results.filter((r) => r.status === "failed").length,
      batchSize: limit,
      totalBatches: Math.ceil(userIds.length / limit),
    };

    console.log("📊 Concurrent with Limit Summary:", summary);
    return { results, summary };
  }
}

// Usage Examples
console.log("✨ Starting Async/Await Demo...");
AsyncAwaitDemo.demonstrateAsyncAwait("20230001")
  .then((result) => {
    console.log("🎊 Async/Await completed:", result.stats.status);
  })
  .catch((error) => {
    console.error("💥 Demo failed:", error.message);
  });

// Parallel execution
console.log("\n🚀 Starting Parallel Execution Demo...");
AsyncAwaitDemo.demonstrateParallelExecution([
  "20230001",
  "20230002",
  "20230003",
]).then((result) => {
  console.log("🎊 Parallel execution completed:", result.summary);
});

// Error handling
console.log("\n🛡️ Starting Error Handling Demo...");
AsyncAwaitDemo.demonstrateErrorHandling([
  "20230001",
  "invalid",
  "20230003",
  "20230004",
]).then((result) => {
  console.log("🎊 Error handling completed:", result.summary);
});

// Concurrent with limit
console.log("\n🎛️ Starting Concurrent with Limit Demo...");
AsyncAwaitDemo.demonstrateConcurrentWithLimit(
  ["20230001", "20230002", "20230003", "20230004", "20230005"],
  2
).then((result) => {
  console.log("🎊 Concurrent with limit completed:", result.summary);
});
```

## 🌐 **Real-world API Integration**

### **Fetch API - Modern HTTP Client**

```javascript
class APIClient {
  constructor(baseURL) {
    this.baseURL = baseURL;
    this.defaultHeaders = {
      "Content-Type": "application/json",
      Accept: "application/json",
    };
  }

  // GET request dengan error handling
  async get(endpoint, options = {}) {
    try {
      console.log(`📡 GET ${this.baseURL}${endpoint}`);

      const response = await fetch(`${this.baseURL}${endpoint}`, {
        method: "GET",
        headers: {
          ...this.defaultHeaders,
          ...options.headers,
        },
        ...options,
      });

      if (!response.ok) {
        throw new Error(`HTTP ${response.status}: ${response.statusText}`);
      }

      const data = await response.json();
      console.log(`✅ GET ${endpoint} berhasil`);
      return data;
    } catch (error) {
      console.error(`❌ GET ${endpoint} gagal:`, error.message);
      throw error;
    }
  }

  // POST request dengan data
  async post(endpoint, data, options = {}) {
    try {
      console.log(`📤 POST ${this.baseURL}${endpoint}`);

      const response = await fetch(`${this.baseURL}${endpoint}`, {
        method: "POST",
        headers: {
          ...this.defaultHeaders,
          ...options.headers,
        },
        body: JSON.stringify(data),
        ...options,
      });

      if (!response.ok) {
        throw new Error(`HTTP ${response.status}: ${response.statusText}`);
      }

      const result = await response.json();
      console.log(`✅ POST ${endpoint} berhasil`);
      return result;
    } catch (error) {
      console.error(`❌ POST ${endpoint} gagal:`, error.message);
      throw error;
    }
  }

  // PUT request untuk update
  async put(endpoint, data, options = {}) {
    try {
      console.log(`📝 PUT ${this.baseURL}${endpoint}`);

      const response = await fetch(`${this.baseURL}${endpoint}`, {
        method: "PUT",
        headers: {
          ...this.defaultHeaders,
          ...options.headers,
        },
        body: JSON.stringify(data),
        ...options,
      });

      if (!response.ok) {
        throw new Error(`HTTP ${response.status}: ${response.statusText}`);
      }

      const result = await response.json();
      console.log(`✅ PUT ${endpoint} berhasil`);
      return result;
    } catch (error) {
      console.error(`❌ PUT ${endpoint} gagal:`, error.message);
      throw error;
    }
  }

  // DELETE request
  async delete(endpoint, options = {}) {
    try {
      console.log(`🗑️ DELETE ${this.baseURL}${endpoint}`);

      const response = await fetch(`${this.baseURL}${endpoint}`, {
        method: "DELETE",
        headers: {
          ...this.defaultHeaders,
          ...options.headers,
        },
        ...options,
      });

      if (!response.ok) {
        throw new Error(`HTTP ${response.status}: ${response.statusText}`);
      }

      // DELETE might not return JSON
      const result = response.status === 204 ? null : await response.json();
      console.log(`✅ DELETE ${endpoint} berhasil`);
      return result;
    } catch (error) {
      console.error(`❌ DELETE ${endpoint} gagal:`, error.message);
      throw error;
    }
  }
}

// Student API Service
class StudentAPIService {
  constructor() {
    this.api = new APIClient("https://api.university.edu/v1");
  }

  // Get all students
  async getAllStudents(filters = {}) {
    const queryParams = new URLSearchParams(filters).toString();
    const endpoint = `/students${queryParams ? "?" + queryParams : ""}`;
    return await this.api.get(endpoint);
  }

  // Get student by ID
  async getStudent(studentId) {
    return await this.api.get(`/students/${studentId}`);
  }

  // Create new student
  async createStudent(studentData) {
    return await this.api.post("/students", studentData);
  }

  // Update student
  async updateStudent(studentId, updateData) {
    return await this.api.put(`/students/${studentId}`, updateData);
  }

  // Delete student
  async deleteStudent(studentId) {
    return await this.api.delete(`/students/${studentId}`);
  }

  // Get student courses
  async getStudentCourses(studentId) {
    return await this.api.get(`/students/${studentId}/courses`);
  }

  // Enroll student in course
  async enrollInCourse(studentId, courseId) {
    return await this.api.post(`/students/${studentId}/courses`, { courseId });
  }

  // Get student grades
  async getStudentGrades(studentId, semester = null) {
    const params = semester ? { semester } : {};
    const queryParams = new URLSearchParams(params).toString();
    const endpoint = `/students/${studentId}/grades${
      queryParams ? "?" + queryParams : ""
    }`;
    return await this.api.get(endpoint);
  }
}

// Complete Student Dashboard Example
class StudentDashboard {
  constructor() {
    this.studentAPI = new StudentAPIService();
    this.currentStudent = null;
  }

  // Load complete student dashboard
  async loadStudentDashboard(studentId) {
    console.log("🎓 Loading Student Dashboard...");

    try {
      // Start multiple requests in parallel
      console.log("🔄 Loading student data in parallel...");

      const [student, courses, grades] = await Promise.all([
        this.studentAPI.getStudent(studentId),
        this.studentAPI.getStudentCourses(studentId),
        this.studentAPI.getStudentGrades(studentId),
      ]);

      this.currentStudent = student;

      // Process and combine data
      const dashboard = {
        student,
        courses,
        grades,
        statistics: this.calculateStatistics(courses, grades),
        lastUpdated: new Date().toISOString(),
      };

      console.log("✅ Student Dashboard loaded successfully");
      console.log("📊 Dashboard Summary:", {
        studentName: student.name,
        totalCourses: courses.length,
        currentGPA: dashboard.statistics.gpa,
        status: dashboard.statistics.status,
      });

      return dashboard;
    } catch (error) {
      console.error("💥 Failed to load student dashboard:", error.message);
      throw error;
    }
  }

  // Update student profile
  async updateStudentProfile(studentId, updateData) {
    console.log("📝 Updating student profile...");

    try {
      const updatedStudent = await this.studentAPI.updateStudent(
        studentId,
        updateData
      );

      console.log("✅ Student profile updated successfully");
      console.log("👤 Updated data:", updatedStudent);

      // Refresh current student data
      this.currentStudent = updatedStudent;

      return updatedStudent;
    } catch (error) {
      console.error("💥 Failed to update student profile:", error.message);
      throw error;
    }
  }

  // Enroll in multiple courses
  async enrollInMultipleCourses(studentId, courseIds) {
    console.log(`📚 Enrolling in ${courseIds.length} courses...`);

    try {
      // Enroll in courses sequentially to avoid conflicts
      const enrollmentResults = [];

      for (const courseId of courseIds) {
        try {
          console.log(`🔄 Enrolling in course ${courseId}...`);
          const result = await this.studentAPI.enrollInCourse(
            studentId,
            courseId
          );
          enrollmentResults.push({ courseId, status: "success", result });
          console.log(`✅ Successfully enrolled in ${courseId}`);
        } catch (error) {
          console.error(`❌ Failed to enroll in ${courseId}:`, error.message);
          enrollmentResults.push({
            courseId,
            status: "failed",
            error: error.message,
          });
        }
      }

      const summary = {
        total: courseIds.length,
        successful: enrollmentResults.filter((r) => r.status === "success")
          .length,
        failed: enrollmentResults.filter((r) => r.status === "failed").length,
      };

      console.log("📊 Enrollment Summary:", summary);

      return { enrollmentResults, summary };
    } catch (error) {
      console.error("💥 Enrollment process failed:", error.message);
      throw error;
    }
  }

  // Calculate student statistics
  calculateStatistics(courses, grades) {
    if (!grades || grades.length === 0) {
      return { gpa: 0, totalCredits: 0, status: "No grades available" };
    }

    const totalCredits = courses.reduce(
      (sum, course) => sum + (course.credits || 0),
      0
    );
    const weightedGrades = grades.reduce((sum, grade) => {
      const course = courses.find((c) => c.id === grade.courseId);
      const credits = course ? course.credits : 0;
      return sum + grade.gradePoint * credits;
    }, 0);

    const gpa = totalCredits > 0 ? weightedGrades / totalCredits : 0;

    let status = "Poor";
    if (gpa >= 3.5) status = "Excellent";
    else if (gpa >= 3.0) status = "Good";
    else if (gpa >= 2.5) status = "Satisfactory";

    return {
      gpa: parseFloat(gpa.toFixed(2)),
      totalCredits,
      status,
      completedCourses: grades.filter((g) => g.completed).length,
      averageScore: grades.reduce((sum, g) => sum + g.score, 0) / grades.length,
    };
  }
}

// Usage Example
async function demonstrateAsyncAPI() {
  console.log("🎓 Starting Student Dashboard Demo...");

  const dashboard = new StudentDashboard();

  try {
    // Load student dashboard
    const studentData = await dashboard.loadStudentDashboard("20230001");

    // Update student profile
    await dashboard.updateStudentProfile("20230001", {
      email: "nazriel.new@email.com",
      phone: "081234567890",
    });

    // Enroll in new courses
    await dashboard.enrollInMultipleCourses("20230001", [
      "MATH201",
      "PHYS101",
      "CHEM101",
    ]);

    console.log("🎊 All async operations completed successfully!");
  } catch (error) {
    console.error("💥 Demo failed:", error.message);
  }
}

// Run the demo
demonstrateAsyncAPI();
```

## 🌟 **Kesimpulan Filosofis**

Asynchronous Programming adalah **jantung aplikasi modern**. Memahami async berarti memahami:

1. **Concurrency vs Parallelism** - Bagaimana mengelola multiple tasks dengan efisien
2. **User Experience** - Bagaimana menjaga responsiveness aplikasi
3. **Resource Management** - Bagaimana mengoptimalkan penggunaan CPU dan network
4. **Error Resilience** - Bagaimana menangani failures dengan graceful

**Philosophy**: "In the symphony of modern web applications, async programming is the conductor that ensures every note plays at the right time, creating harmony from complexity."

Async mengajarkan kita bahwa **patience and timing** adalah virtue dalam programming, dan bahwa **waiting intelligently** adalah lebih baik daripada **blocking stupidly**. ⏰✨

---

## 📁 **File Praktikum dalam Folder**

1. `01-callback-basics.html` - Dasar callback dan event handling
2. `02-promises.html` - Promise implementation dengan contoh Indonesia
3. `03-async-await.html` - Modern async/await patterns
4. `04-fetch-api.html` - HTTP requests dengan Fetch API
5. `05-error-handling.html` - Error handling strategies dalam async code
6. `06-real-time-data.html` - Real-time data updates dengan polling
7. `studi-kasus-weather-app.html` - Aplikasi cuaca dengan async API calls

## 🎯 **Tujuan Pembelajaran**

Memahami dan menguasai asynchronous programming dalam JavaScript, dari callback sampai async/await, dan mengintegrasikan dengan real-world APIs untuk membangun aplikasi yang responsif dan modern.);
console.log("End"); // This executes immediately

```

### 2. JavaScript Event Loop

#### Konsep Event Loop:
JavaScript adalah single-threaded, tetapi dapat menangani operasi asynchronous melalui event loop.

```

┌───────────────────────────┐
┌─>│ timers │ ← setTimeout, setInterval
│ └─────────────┬─────────────┘
│ ┌─────────────┴─────────────┐
│ │ pending callbacks │ ← I/O callbacks
│ └─────────────┬─────────────┘
│ ┌─────────────┴─────────────┐
│ │ idle, prepare │ ← Internal use
│ └─────────────┬─────────────┘
│ ┌─────────────┴─────────────┐
│ │ poll │ ← Fetching new I/O events
│ └─────────────┬─────────────┘
│ ┌─────────────┴─────────────┐
│ │ check │ ← setImmediate callbacks
│ └─────────────┬─────────────┘
│ ┌─────────────┴─────────────┐
└──┤ close callbacks │
└───────────────────────────┘

````

#### Call Stack, Web APIs, dan Callback Queue:
```javascript
// Example of event loop in action
console.log("1"); // Call stack

setTimeout(() => {
    console.log("2"); // Web API → Callback Queue → Call Stack
}, 0);

Promise.resolve().then(() => {
    console.log("3"); // Microtask Queue (higher priority)
});

console.log("4"); // Call stack

// Output: 1, 4, 3, 2
````

### 3. Callbacks dan Callback Hell

#### Basic Callbacks:

```javascript
function fetchUser(id, callback) {
  setTimeout(() => {
    const user = { id, name: "Nazriel Rahman Al'afath" };
    callback(null, user); // Error-first callback pattern
  }, 1000);
}

// Usage
fetchUser(1, (error, user) => {
  if (error) {
    console.error("Error:", error);
  } else {
    console.log("User:", user);
  }
});
```

#### Callback Hell Problem:

```javascript
// Nested callbacks become difficult to read and maintain
fetchUser(1, (error, user) => {
  if (error) {
    handleError(error);
  } else {
    fetchUserPosts(user.id, (error, posts) => {
      if (error) {
        handleError(error);
      } else {
        fetchPostComments(posts[0].id, (error, comments) => {
          if (error) {
            handleError(error);
          } else {
            // Finally, we have the data we need
            console.log("Comments:", comments);
          }
        });
      }
    });
  }
});
```

### 4. Promises

#### Promise States:

- **Pending**: Initial state, neither fulfilled nor rejected
- **Fulfilled**: Operation completed successfully
- **Rejected**: Operation failed

```javascript
// Creating a Promise
const myPromise = new Promise((resolve, reject) => {
  // Asynchronous operation
  const success = Math.random() > 0.5;

  setTimeout(() => {
    if (success) {
      resolve("Operation successful!"); // Fulfill the promise
    } else {
      reject(new Error("Operation failed!")); // Reject the promise
    }
  }, 1000);
});
```

#### Promise Methods:

```javascript
// then() - Handle fulfilled state
myPromise.then((result) => {
  console.log("Success:", result);
});

// catch() - Handle rejected state
myPromise.catch((error) => {
  console.error("Error:", error);
});

// finally() - Always executed
myPromise.finally(() => {
  console.log("Cleanup operations");
});

// Chaining methods
myPromise
  .then((result) => {
    console.log("Success:", result);
    return "Modified result";
  })
  .then((modifiedResult) => {
    console.log("Modified:", modifiedResult);
  })
  .catch((error) => {
    console.error("Error:", error);
  })
  .finally(() => {
    console.log("Done");
  });
```

#### Promise Chaining:

```javascript
// Solving callback hell with promises
fetchUser(1)
  .then((user) => {
    console.log("User:", user);
    return fetchUserPosts(user.id);
  })
  .then((posts) => {
    console.log("Posts:", posts);
    return fetchPostComments(posts[0].id);
  })
  .then((comments) => {
    console.log("Comments:", comments);
  })
  .catch((error) => {
    console.error("Error in chain:", error);
  });
```

#### Static Promise Methods:

```javascript
// Promise.resolve() - Create resolved promise
const resolvedPromise = Promise.resolve("Immediate value");

// Promise.reject() - Create rejected promise
const rejectedPromise = Promise.reject(new Error("Immediate error"));

// Promise.all() - Wait for all promises
const promises = [fetchUser(1), fetchUser(2), fetchUser(3)];

Promise.all(promises)
  .then((users) => {
    console.log("All users:", users);
  })
  .catch((error) => {
    console.error("One promise failed:", error);
  });

// Promise.allSettled() - Wait for all, regardless of outcome
Promise.allSettled(promises).then((results) => {
  results.forEach((result, index) => {
    if (result.status === "fulfilled") {
      console.log(`Promise ${index} succeeded:`, result.value);
    } else {
      console.log(`Promise ${index} failed:`, result.reason);
    }
  });
});

// Promise.race() - First settled promise wins
Promise.race(promises).then((firstUser) => {
  console.log("First user received:", firstUser);
});

// Promise.any() - First fulfilled promise wins
Promise.any(promises)
  .then((firstSuccessfulUser) => {
    console.log("First successful user:", firstSuccessfulUser);
  })
  .catch((error) => {
    console.error("All promises rejected:", error);
  });
```

### 5. Async/Await

#### Basic Syntax:

```javascript
// Function marked as async returns a Promise
async function fetchUserData() {
  try {
    // await pauses execution until Promise resolves
    const user = await fetchUser(1);
    const posts = await fetchUserPosts(user.id);
    const comments = await fetchPostComments(posts[0].id);

    return {
      user,
      posts,
      comments,
    };
  } catch (error) {
    console.error("Error fetching data:", error);
    throw error; // Re-throw if needed
  }
}

// Using the async function
fetchUserData()
  .then((data) => {
    console.log("Complete data:", data);
  })
  .catch((error) => {
    console.error("Failed to fetch data:", error);
  });
```

#### Parallel Execution with Async/Await:

```javascript
// Sequential execution (slow)
async function fetchDataSequential() {
  const user1 = await fetchUser(1); // Wait 1 second
  const user2 = await fetchUser(2); // Wait another 1 second
  const user3 = await fetchUser(3); // Wait another 1 second
  // Total: ~3 seconds

  return [user1, user2, user3];
}

// Parallel execution (fast)
async function fetchDataParallel() {
  const [user1, user2, user3] = await Promise.all([
    fetchUser(1), // All three start simultaneously
    fetchUser(2),
    fetchUser(3),
  ]);
  // Total: ~1 second

  return [user1, user2, user3];
}
```

#### Error Handling with Async/Await:

```javascript
async function robustDataFetch() {
  try {
    const user = await fetchUser(1);

    try {
      const posts = await fetchUserPosts(user.id);
      return { user, posts };
    } catch (postsError) {
      // Handle posts error specifically
      console.warn("Could not fetch posts:", postsError);
      return { user, posts: [] };
    }
  } catch (userError) {
    // Handle user fetch error
    console.error("Could not fetch user:", userError);
    throw new Error("User data is required");
  }
}
```

### 6. Fetch API

#### Basic Fetch Usage:

```javascript
// GET request
fetch("https://api.example.com/users")
  .then((response) => {
    // Check if request was successful
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    return response.json();
  })
  .then((data) => {
    console.log("Users:", data);
  })
  .catch((error) => {
    console.error("Fetch error:", error);
  });
```

#### Fetch with Async/Await:

```javascript
async function fetchUsers() {
  try {
    const response = await fetch("https://api.example.com/users");

    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    const users = await response.json();
    return users;
  } catch (error) {
    console.error("Error fetching users:", error);
    throw error;
  }
}
```

#### HTTP Methods with Fetch:

```javascript
// POST request
async function createUser(userData) {
  try {
    const response = await fetch("https://api.example.com/users", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer " + getAuthToken(),
      },
      body: JSON.stringify(userData),
    });

    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    return await response.json();
  } catch (error) {
    console.error("Error creating user:", error);
    throw error;
  }
}

// PUT request
async function updateUser(id, userData) {
  const response = await fetch(`https://api.example.com/users/${id}`, {
    method: "PUT",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(userData),
  });

  return response.json();
}

// DELETE request
async function deleteUser(id) {
  const response = await fetch(`https://api.example.com/users/${id}`, {
    method: "DELETE",
  });

  return response.ok;
}
```

#### Request Configuration:

```javascript
// Advanced fetch configuration
const requestConfig = {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    Authorization: "Bearer token",
    "X-Custom-Header": "value",
  },
  body: JSON.stringify(data),
  mode: "cors", // cors, no-cors, same-origin
  credentials: "include", // include, same-origin, omit
  cache: "no-cache", // default, no-cache, reload, force-cache
  redirect: "follow", // follow, error, manual
  referrerPolicy: "no-referrer", // no-referrer, origin, etc.
};

const response = await fetch(url, requestConfig);
```

### 7. Error Handling Strategies

#### Try-Catch Patterns:

```javascript
// Basic error handling
async function handleErrors() {
  try {
    const data = await fetchData();
    return data;
  } catch (error) {
    console.error("Error:", error);
    // Decide how to handle the error
    throw error; // Re-throw
    // or return default value
    // return { error: true, message: error.message };
  }
}

// Multiple try-catch blocks
async function complexOperation() {
  let user, posts, comments;

  try {
    user = await fetchUser(1);
  } catch (error) {
    console.error("User fetch failed:", error);
    throw new Error("Cannot proceed without user data");
  }

  try {
    posts = await fetchUserPosts(user.id);
  } catch (error) {
    console.warn("Posts fetch failed, using empty array:", error);
    posts = [];
  }

  try {
    if (posts.length > 0) {
      comments = await fetchPostComments(posts[0].id);
    }
  } catch (error) {
    console.warn("Comments fetch failed:", error);
    comments = [];
  }

  return { user, posts, comments };
}
```

#### Retry Logic:

```javascript
async function fetchWithRetry(url, options = {}, maxRetries = 3) {
  let lastError;

  for (let attempt = 1; attempt <= maxRetries; attempt++) {
    try {
      const response = await fetch(url, options);

      if (!response.ok) {
        throw new Error(`HTTP ${response.status}: ${response.statusText}`);
      }

      return response;
    } catch (error) {
      lastError = error;

      if (attempt === maxRetries) {
        throw error;
      }

      // Exponential backoff
      const delay = Math.pow(2, attempt - 1) * 1000;
      console.log(`Attempt ${attempt} failed. Retrying in ${delay}ms...`);
      await new Promise((resolve) => setTimeout(resolve, delay));
    }
  }

  throw lastError;
}
```

#### Circuit Breaker Pattern:

```javascript
class CircuitBreaker {
  constructor(threshold = 5, timeout = 60000) {
    this.threshold = threshold;
    this.timeout = timeout;
    this.failureCount = 0;
    this.lastFailureTime = null;
    this.state = "CLOSED"; // CLOSED, OPEN, HALF_OPEN
  }

  async call(fn) {
    if (this.state === "OPEN") {
      if (this.canAttemptReset()) {
        this.state = "HALF_OPEN";
      } else {
        throw new Error("Circuit breaker is OPEN");
      }
    }

    try {
      const result = await fn();
      this.onSuccess();
      return result;
    } catch (error) {
      this.onFailure();
      throw error;
    }
  }

  onSuccess() {
    this.failureCount = 0;
    this.state = "CLOSED";
  }

  onFailure() {
    this.failureCount++;
    this.lastFailureTime = Date.now();

    if (this.failureCount >= this.threshold) {
      this.state = "OPEN";
    }
  }

  canAttemptReset() {
    return Date.now() - this.lastFailureTime >= this.timeout;
  }
}
```

### 8. Request Timeout and Cancellation

#### AbortController for Cancellation:

```javascript
// Create abort controller
const controller = new AbortController();
const signal = controller.signal;

// Make request with abort signal
const response = await fetch(url, { signal });

// Cancel the request
controller.abort();

// Handle cancellation
try {
  const data = await response.json();
} catch (error) {
  if (error.name === "AbortError") {
    console.log("Request was cancelled");
  } else {
    console.error("Other error:", error);
  }
}
```

#### Timeout Implementation:

```javascript
async function fetchWithTimeout(url, timeout = 5000) {
  const controller = new AbortController();
  const timeoutId = setTimeout(() => controller.abort(), timeout);

  try {
    const response = await fetch(url, {
      signal: controller.signal,
    });

    clearTimeout(timeoutId);
    return response;
  } catch (error) {
    clearTimeout(timeoutId);

    if (error.name === "AbortError") {
      throw new Error(`Request timeout after ${timeout}ms`);
    }

    throw error;
  }
}
```

### 9. Performance Optimization

#### Request Batching:

```javascript
class RequestBatcher {
  constructor(batchSize = 10, delay = 100) {
    this.batchSize = batchSize;
    this.delay = delay;
    this.queue = [];
    this.timer = null;
  }

  add(request) {
    return new Promise((resolve, reject) => {
      this.queue.push({ request, resolve, reject });

      if (this.queue.length >= this.batchSize) {
        this.flush();
      } else if (!this.timer) {
        this.timer = setTimeout(() => this.flush(), this.delay);
      }
    });
  }

  async flush() {
    if (this.timer) {
      clearTimeout(this.timer);
      this.timer = null;
    }

    const batch = this.queue.splice(0, this.batchSize);

    if (batch.length === 0) return;

    try {
      const results = await this.executeBatch(
        batch.map((item) => item.request)
      );

      batch.forEach((item, index) => {
        item.resolve(results[index]);
      });
    } catch (error) {
      batch.forEach((item) => {
        item.reject(error);
      });
    }
  }

  async executeBatch(requests) {
    // Execute all requests in parallel
    return Promise.all(
      requests.map((request) => fetch(request.url, request.options))
    );
  }
}
```

#### Caching Strategies:

```javascript
class ApiCache {
  constructor(ttl = 5 * 60 * 1000) {
    // 5 minutes default TTL
    this.cache = new Map();
    this.ttl = ttl;
  }

  async get(key, fetcher) {
    const cached = this.cache.get(key);

    if (cached && Date.now() - cached.timestamp < this.ttl) {
      return cached.data;
    }

    try {
      const data = await fetcher();
      this.cache.set(key, {
        data,
        timestamp: Date.now(),
      });
      return data;
    } catch (error) {
      // Return stale data if available
      if (cached) {
        console.warn("Using stale cache due to error:", error);
        return cached.data;
      }
      throw error;
    }
  }

  clear() {
    this.cache.clear();
  }

  delete(key) {
    this.cache.delete(key);
  }
}

// Usage
const cache = new ApiCache();

async function fetchUser(id) {
  return cache.get(`user:${id}`, async () => {
    const response = await fetch(`/api/users/${id}`);
    return response.json();
  });
}
```

### 10. Real-time Communication

#### Server-Sent Events (SSE):

```javascript
function connectToEventStream(url) {
  const eventSource = new EventSource(url);

  eventSource.onopen = function (event) {
    console.log("Connection opened");
  };

  eventSource.onmessage = function (event) {
    const data = JSON.parse(event.data);
    console.log("Received:", data);
  };

  eventSource.onerror = function (event) {
    console.error("EventSource error:", event);
  };

  // Custom event types
  eventSource.addEventListener("user-update", function (event) {
    const userData = JSON.parse(event.data);
    updateUserInterface(userData);
  });

  return eventSource;
}
```

#### WebSockets:

```javascript
class WebSocketClient {
  constructor(url) {
    this.url = url;
    this.ws = null;
    this.reconnectAttempts = 0;
    this.maxReconnectAttempts = 5;
    this.reconnectDelay = 1000;
  }

  connect() {
    return new Promise((resolve, reject) => {
      this.ws = new WebSocket(this.url);

      this.ws.onopen = () => {
        console.log("WebSocket connected");
        this.reconnectAttempts = 0;
        resolve();
      };

      this.ws.onmessage = (event) => {
        const data = JSON.parse(event.data);
        this.handleMessage(data);
      };

      this.ws.onclose = () => {
        console.log("WebSocket disconnected");
        this.attemptReconnect();
      };

      this.ws.onerror = (error) => {
        console.error("WebSocket error:", error);
        reject(error);
      };
    });
  }

  send(data) {
    if (this.ws && this.ws.readyState === WebSocket.OPEN) {
      this.ws.send(JSON.stringify(data));
    } else {
      console.warn("WebSocket not connected");
    }
  }

  attemptReconnect() {
    if (this.reconnectAttempts < this.maxReconnectAttempts) {
      this.reconnectAttempts++;
      const delay =
        this.reconnectDelay * Math.pow(2, this.reconnectAttempts - 1);

      console.log(
        `Reconnecting in ${delay}ms... (attempt ${this.reconnectAttempts})`
      );

      setTimeout(() => {
        this.connect().catch(console.error);
      }, delay);
    } else {
      console.error("Max reconnection attempts reached");
    }
  }

  handleMessage(data) {
    // Override this method to handle incoming messages
    console.log("Received message:", data);
  }

  close() {
    if (this.ws) {
      this.ws.close();
    }
  }
}
```

## 🎯 Modern Async Patterns

### 1. **Async Generators**

```javascript
async function* dataStream() {
  let page = 1;

  while (true) {
    const response = await fetch(`/api/data?page=${page}`);
    const data = await response.json();

    if (data.items.length === 0) break;

    yield data.items;
    page++;
  }
}

// Usage
for await (const items of dataStream()) {
  console.log("Processing batch:", items);
}
```

### 2. **Promise-based Queues**

```javascript
class AsyncQueue {
  constructor(concurrency = 1) {
    this.concurrency = concurrency;
    this.running = 0;
    this.queue = [];
  }

  async add(fn) {
    return new Promise((resolve, reject) => {
      this.queue.push({
        fn,
        resolve,
        reject,
      });

      this.process();
    });
  }

  async process() {
    if (this.running >= this.concurrency || this.queue.length === 0) {
      return;
    }

    this.running++;
    const { fn, resolve, reject } = this.queue.shift();

    try {
      const result = await fn();
      resolve(result);
    } catch (error) {
      reject(error);
    } finally {
      this.running--;
      this.process();
    }
  }
}
```

## 🔧 Best Practices

### 1. **Error Boundaries**

```javascript
// Global error handler for unhandled promise rejections
window.addEventListener("unhandledrejection", function (event) {
  console.error("Unhandled promise rejection:", event.reason);
  // Report to error tracking service
  event.preventDefault(); // Prevent default browser behavior
});
```

### 2. **Loading States**

```javascript
async function handleAsyncOperation() {
  const loadingState = {
    loading: true,
    error: null,
    data: null,
  };

  updateUI(loadingState);

  try {
    const data = await fetchData();
    updateUI({
      loading: false,
      error: null,
      data,
    });
  } catch (error) {
    updateUI({
      loading: false,
      error: error.message,
      data: null,
    });
  }
}
```

### 3. **Resource Management**

```javascript
// Cleanup pattern for async operations
class AsyncResourceManager {
  constructor() {
    this.activeRequests = new Set();
    this.intervals = new Set();
    this.timeouts = new Set();
  }

  async fetch(url, options = {}) {
    const controller = new AbortController();
    const request = fetch(url, {
      ...options,
      signal: controller.signal,
    });

    this.activeRequests.add(controller);

    try {
      const response = await request;
      return response;
    } finally {
      this.activeRequests.delete(controller);
    }
  }

  setInterval(callback, delay) {
    const id = setInterval(callback, delay);
    this.intervals.add(id);
    return id;
  }

  setTimeout(callback, delay) {
    const id = setTimeout(() => {
      callback();
      this.timeouts.delete(id);
    }, delay);
    this.timeouts.add(id);
    return id;
  }

  cleanup() {
    // Cancel all active requests
    this.activeRequests.forEach((controller) => controller.abort());
    this.activeRequests.clear();

    // Clear all intervals
    this.intervals.forEach((id) => clearInterval(id));
    this.intervals.clear();

    // Clear all timeouts
    this.timeouts.forEach((id) => clearTimeout(id));
    this.timeouts.clear();
  }
}
```

## 📝 Latihan Praktik

### 1. **Promise Fundamentals**

- Creating and chaining promises
- Error handling with catch
- Promise.all vs Promise.race

### 2. **Async/Await Mastery**

- Converting promises to async/await
- Error handling with try/catch
- Parallel vs sequential execution

### 3. **Fetch API Usage**

- GET, POST, PUT, DELETE requests
- Request headers and authentication
- Response handling and error cases

### 4. **Real-world Applications**

- API integration
- Real-time data updates
- Error recovery patterns
- Performance optimization

Memahami asynchronous programming adalah kunci untuk membangun aplikasi web modern yang responsif dan dapat menangani operasi I/O secara efisien.
