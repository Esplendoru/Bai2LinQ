using System;
using System.Collections.Generic;
using System.Linq;

namespace QuanLyDSHocSinh_LinQ
{
    public class Student
    {
        public int Id { get; set; }
        public string Name { get; set; }
        public int Age { get; set; }

        public override string ToString()
        {
            return $"Id: {Id,-3} | Name: {Name,-8} | Age: {Age}";
        }
    }

    public class Program
    {
        static void Main(string[] args)
        {
            var students = new List<Student>
            {
                new Student { Id = 1, Name = "Huy", Age = 16 },
                new Student { Id = 2, Name = "Viet", Age = 14 },
                new Student { Id = 3, Name = "Thang", Age = 18 },
                new Student { Id = 4, Name = "Minh", Age = 15 },
                new Student { Id = 5, Name = "Hieu", Age = 19 },
                new Student { Id = 6, Name = "Hoang", Age = 16 }
            };

            HienThiToanBoHocSinh(students);
            HienThiHocSinhTheoDoTuoi(students, 15, 18);
            HienThiHocSinhTheoTenBatDau(students, "H");
            TinhVaInTongSoTuoi(students);
            HienThiHocSinhLonTuoiNhat(students);
            HienThiDanhSachSapXepTheoTuoi(students);
        }

        private static void HienThiToanBoHocSinh(List<Student> students)
        {
            Console.WriteLine("a. Danh sach hoc sinh:");
            foreach (var s in students)
            {
                Console.WriteLine(s);
            }
            Console.WriteLine();
        }

        private static void HienThiHocSinhTheoDoTuoi(List<Student> students, int minAge, int maxAge)
        {
            Console.WriteLine($"b. Hoc sinh tuoi tu {minAge} den {maxAge}:");
            var studentsByAge = students.Where(s => s.Age >= minAge && s.Age <= maxAge);

            if (!studentsByAge.Any())
            {
                Console.WriteLine("Khong tim thay hoc sinh nao trong do tuoi nay.");
            }
            else
            {
                foreach (var s in studentsByAge)
                {
                    Console.WriteLine(s);
                }
            }
            Console.WriteLine();
        }

        private static void HienThiHocSinhTheoTenBatDau(List<Student> students, string startingChar)
        {
            Console.WriteLine($"c. Hoc sinh co ten bat dau bang '{startingChar}':");
            var studentsByName = students.Where(s => s.Name.StartsWith(startingChar, StringComparison.OrdinalIgnoreCase));

            if (!studentsByName.Any())
            {
                Console.WriteLine($"Khong tim thay hoc sinh nao co ten bat dau bang '{startingChar}'.");
            }
            else
            {
                foreach (var s in studentsByName)
                {
                    Console.WriteLine(s);
                }
            }
            Console.WriteLine();
        }

        private static void TinhVaInTongSoTuoi(List<Student> students)
        {
            Console.WriteLine("d. Tong tuoi tat ca hoc sinh trong danh sach:");
            int totalAge = students.Sum(s => s.Age);
            Console.WriteLine($"Tong so tuoi = {totalAge}");
            Console.WriteLine();
        }

        private static void HienThiHocSinhLonTuoiNhat(List<Student> students)
        {
            Console.WriteLine("e. Hoc sinh co tuoi lon nhat:");
            int maxAge = students.Max(s => s.Age);
            var oldestStudents = students.Where(s => s.Age == maxAge);
            
            foreach (var s in oldestStudents)
            {
                Console.WriteLine(s);
            }
            Console.WriteLine();
        }

        private static void HienThiDanhSachSapXepTheoTuoi(List<Student> students)
        {
            Console.WriteLine("f. Danh sach sap xep theo tuoi tang dan:");
            var sortedStudents = students.OrderBy(s => s.Age);
            
            foreach (var s in sortedStudents)
            {
                Console.WriteLine(s);
            }
            Console.WriteLine();
        }
    }
}
