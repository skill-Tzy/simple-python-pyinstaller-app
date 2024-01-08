# Intermediate-DevOps Engineer

Submission Proyek Membangun CI/CD Pipeline dengan Jenkins - Kelas Belajar Implementasi CI/CD

[Sertifikat Kompetensi Kelas Belajar Implementasi CI/CD](https://www.dicoding.com/certificates/0LZ0265N3X65)

## 🚀 Deskripsi Kelas

Kelas Belajar Implementasi CI/CD <br>
Disusun oleh: Dicoding Indonesia <br>
Level: Menengah

<div align="center">
  <img src="https://user-images.githubusercontent.com/95717485/225231893-e59de44d-0d3e-4e79-971b-a4d494565a74.png" alt="Dicoding AWS">
</div>

<br>

- **Pengenalan CI/CD** : Mengetahui pengertian, alur, dan manfaat dari implementasi CI/CD. (1 jam)
- **Continuous Integration** : Memahami dua model jaringan yang umum di dunia jaringan komputer, yakni model OSI dan model TCP/IP. (2 jam 45 menit)
- **Continuous Deployment** : Memahami pengertian dan implementasi continous deployment. (4 jam)
- **Operation dan Monitoring** : Memahami cara dalam mengoperasikan dan memonitor baik aplikasi maupun infrastruktur. (3 jam 15 menit)
- **DevSecOps** : Mengetahui apa itu DevSecOps dan bagaimana cara menerapkan keamanan pada CI/CD pipeline. (1 jam 30 menit)

Evaluasi Pembelajaran:

- Ujian akhir kelas
- Submission (Proyek Akhir) berupa tugas untuk membuat CI/CD pipeline menggunakan Jenkins dengan menerapkan kriteria-kriteria yang telah ditentukan.
  
Total jam yang dibutuhkan untuk menyelesaikan kelas ini adalah 30 jam.

# simple-python-pyinstaller-app

This repository is for the
[Build a Python app with PyInstaller](https://jenkins.io/doc/tutorials/build-a-python-app-with-pyinstaller/)
tutorial in the [Jenkins User Documentation](https://jenkins.io/doc/).

The repository contains a simple Python application which is a command line tool "add2vals" that outputs the addition of two values. If at least one of the
values is a string, "add2vals" treats both values as a string and instead
concatenates the values. The "add2" function in the "calc" library (which
"add2vals" imports) is accompanied by a set of unit tests. These are tested with pytest to check that this function works as expected and the results are saved
to a JUnit XML report.

The delivery of the "add2vals" tool through PyInstaller converts this tool into
a standalone executable file for Linux, which you can download through Jenkins
and execute at the command line on Linux machines without Python.

The `jenkins` directory contains an example of the `Jenkinsfile` (i.e. Pipeline)
you'll be creating yourself during the tutorial.
