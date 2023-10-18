# DateTimeClass
Create by - Денис Казанцев & Артем Николаев
///

Задание:

1- Создать метод PrevDate()  определяющий дату предыдущего дня. Метод имеет входящий параметр DateTime 

2- Создать метод NextDate() определяющий дату следующего дня. Метод имеет входящий параметр DateTime

3- Создать метод DaysUntilEndMonth(), который позволяет определить сколько дней осталось до конца месяца. Метод имеет входящий параметр DateTime

4- Создать метод LeapYearCheck() , который позволяет определить является ли год високосным

5- Создать метод FindDate(), который позволяет определить дату i-того по счету дня относительно установленной даты (при отрицательных значениях индекса отсчет ведется в обратном порядке). Метод имеет два входящих параметра:  дата относительно которой выполняется поиск, целое значение - число дней, которые необходимо отсчитать от указанной даты

6- Создать метод NextDayOfMonth(), который возвращает значение true, если установленная дата не является последним днем месяца, иначе false;

7- Создать метод FirstDayOdYear(), который выдает значение true, если установленная дата является началом года, иначе false;

8- Создавть метод TimeSpanPeriods(), который выдает сколько временных промежутков (с заданным количеством минут) находится между двумя датами 


///
-Lib

    using System;
    using System.Collections.Generic;
    using System.Globalization;
    using System.Linq;
    using System.Reflection;
    using System.Text;
    using System.Text.RegularExpressions;
    using System.Threading.Tasks;
    
    namespace DateTimeLIb
    {
        public class DateTimeClass
        {
            public static DateTime PrevDate(DateTime date)
            {
                return date.AddDays(-1);
            }
            public static DateTime NextDate(DateTime date)
            {
                return date.AddDays(+1);
            }
            public static int DaysUnitEndMonth(DateTime date)
            {
                return DateTime.DaysInMonth(date.Year, date.Month) - date.Day;
            }
            public static bool LeapYearCheck(DateTime date)
            {
                int z = date.Year;
                
            if (z % 4 ==0)
            {
                return true;
            }
            return false;
        }
        public static DateTime FindDate(DateTime date, int days)
        {
            date = date.AddDays(days);
            return date;
        }
        public static bool NextDayOfMounth(DateTime date)
        {
            int z = DateTime.DaysInMonth(date.Year, date.Month);
            if (date.Day < z)
            {
                return true;
            }
            else
            {
                return false;
            }
        }
        public static bool FirstDayOdYear(DateTime date)
        {
            if (date.DayOfYear == 1)
            {
                return true;
            }
            return false;
        }
        public static int TimeSpanPeriods(DateTime firstDate, DateTime secondDate, int minutes)
        {
            TimeSpan timeSpan = secondDate - firstDate; 
            double minutesCount = timeSpan.TotalMinutes; 
            int period = (int)(minutesCount / minutes); 
            return period;
        }


       }
    }
-TESTS

    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System;
    using DateTimeLIb;
    using Microsoft.VisualBasic;
    
    namespace DateTimTest
    {
        [TestClass]
        public class DateTimee
        {
            
            [TestMethod]
            public void PrevDateTest()
            {
                // Arrange
                DateTime date = new DateTime(2077, 1, 2);
                // Act
                DateTime result = DateTimeClass.PrevDate(date);
                // Assert
                Assert.AreEqual(new DateTime(2077, 1, 1), result);
            }
            [TestMethod]
            public void NextDateTest()
            {
                //Arrange
                DateTime date = new DateTime(2077, 2 , 3);
                //Act
                DateTime result = DateTimeClass.NextDate(date);
                //Assert
                Assert.AreEqual(new DateTime(2077,2, 4), result);
            }
            [TestMethod]
            public void DaysUnitEndMonthTest() 
            {
                // Arrange
                DateTime date = new DateTime(2077, 1, 15);
                // Act
                int result = DateTimeClass.DaysUnitEndMonth(date);
                // Assert
                Assert.AreEqual(16, result);
            }
            [TestMethod]
            public void LeapYearCheckNegativTest()
            {
    
                // Arrange
                DateTime date = new DateTime(2077,1, 1);
                // Act
                bool result = DateTimeClass.LeapYearCheck(date);
                // Assert
                Assert.IsFalse(result);
            }
            [TestMethod]
            public void LeapYearCheckPositivTest()
            {
                // Assert 
                DateTime date = new DateTime(2024, 1, 1);
                // Act
                bool result = DateTimeClass.LeapYearCheck(date);
                // Assert
                Assert.IsTrue(result);
            }
            [TestMethod]
            public void FindDateTest()
            {
                // Arrange
                DateTime date = new DateTime(2077, 9, 1);
                int days = 10;
                // Act
                DateTime result = DateTimeClass.FindDate(date, days);
                // Assert
                Assert.AreEqual(new DateTime(2077, 9, 11), result);
            }
            [TestMethod]
            public void NextDayOfMounthPositiveTest()
            {
                // Arrange
                DateTime date = new DateTime(2023, 10, 18);
                // Act
                bool result = DateTimeClass.NextDayOfMounth(date);
                // Assert
                Assert.IsTrue(result);
            }
            [TestMethod]
            public void NextDayOfMounthNegativeTest()
            {
                // Arrange
                DateTime date = new DateTime(2023, 10, 31);
                // Act
                bool result = DateTimeClass.NextDayOfMounth(date);
                // Assert
                Assert.IsFalse(result);
            }
            [TestMethod]
            public void FirstDayOdYearPositiveTest()
            {
                // Arrange
                DateTime date = new DateTime(2077, 1, 1);
                // Act
                bool result = DateTimeClass.FirstDayOdYear(date);
                // Assert 
                Assert.IsTrue(result);
            }
            [TestMethod]
            public void FirstDayOdYearNegativeTest()
            {
                // Arrange
                DateTime date = new DateTime(2077, 9, 11);
                // Act
                bool result = DateTimeClass.FirstDayOdYear(date);
                // Assert 
                Assert.IsFalse(result);
            }
            [TestMethod]
            public void TimeSpanPeriodsTest()
            {
                // Arrange
                DateTime firstDate = new DateTime(2021, 6, 1);
                DateTime secondDate = new DateTime(2021, 6, 2);
                int z = 24;
                // Act
                int actual = DateTimeClass.TimeSpanPeriods(firstDate, secondDate, 60);
                // Assert 
                Assert.AreEqual(z, actual);
            }
    
        }
    }
