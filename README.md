using System;
using System.Collections.Generic;
 
// Interface tanımı
public interface IPerson
{
    void Login(); // Zorunlu metot
}
 
// Base class tanımı
public abstract class Person : IPerson
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
 
    public abstract void BilgiGoster(); // Polymorphism için abstract metot
 
    public void Login()
    {
        Console.WriteLine($"{Name} giriş yaptı.");
    }
}
 
// Öğrenci sınıfı
public class Ogrenci : Person
{
    public int OgrenciNumarasi { get; set; }
 
    public override void BilgiGoster()
    {
        Console.WriteLine($"Öğrenci: {Name}, Numarası: {OgrenciNumarasi}, Email: {Email}");
    }
}
 
// Öğretim Görevlisi sınıfı
public class OgretimGorevlisi : Person
{
    public string Departman { get; set; }
 
    public override void BilgiGoster()
    {
        Console.WriteLine($"Öğretim Görevlisi: {Name}, Departman: {Departman}, Email: {Email}");
    }
}
 
// Ders sınıfı
public class Course
{
    public string DersAdi { get; set; }
    public int Kredi { get; set; }
    public OgretimGorevlisi OgretimGorevlisi { get; set; }
    public List<Ogrenci> KayitliOgrenciler { get; set; } = new List<Ogrenci>();
 
    public void DersBilgileriGoster()
    {
        Console.WriteLine($"Ders Adı: {DersAdi}, Kredi: {Kredi}");
        Console.WriteLine($"Dersi Veren: {OgretimGorevlisi.Name}");
        Console.WriteLine("Kayıtlı Öğrenciler:");
        foreach (var ogrenci in KayitliOgrenciler)
        {
            Console.WriteLine($" - {ogrenci.Name}");
        }
    }
 
    public void OgrenciKaydet(Ogrenci ogrenci)
    {
        KayitliOgrenciler.Add(ogrenci);
        Console.WriteLine($"{ogrenci.Name}, {DersAdi} dersine kaydedildi.");
    }
}
 
// Main program
class Program
{
    static void Main(string[] args)
    {
        // Öğretim Görevlisi oluşturma
        var ogretimGorevlisi = new OgretimGorevlisi
        {
            Id = 1,
            Name = "Dr. Recep Öztürk",
            Email = "recepozturk@uni.edu.tr",
            Departman = "Bilgisayar Mühendisliği"
        };
 
        // Öğrenci oluşturma
        var ogrenci1 = new Ogrenci
        {
            Id = 101,
            Name = "Ayşe Kaya",
            Email = "ayse.kaya@student.uni.edu.tr",
            OgrenciNumarasi = 20231001
        };
 
        var ogrenci2 = new Ogrenci
        {
            Id = 102,
            Name = "Ali Demir",
            Email = "ali.demir@student.uni.edu.tr",
            OgrenciNumarasi = 20231002
        };
 
        // Ders oluşturma
        var course = new Course
        {
            DersAdi = "Programlama 101",
            Kredi = 4,
            OgretimGorevlisi = ogretimGorevlisi
        };
 
        // Öğrencileri derse kaydetme
        course.OgrenciKaydet(ogrenci1);
        course.OgrenciKaydet(ogrenci2);
 
        // Bilgileri gösterme
        Console.WriteLine("\n=== Bilgiler ===");
        ogretimGorevlisi.BilgiGoster();
        ogrenci1.BilgiGoster();
        ogrenci2.BilgiGoster();
        course.DersBilgileriGoster();
    }
}
