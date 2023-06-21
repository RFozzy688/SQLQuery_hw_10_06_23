CREATE VIEW TeacherAndBookName AS
SELECT t.last_name [Фамилия], b.name [Название книги]
FROM Teacher t JOIN T_Cards t_c
ON t.id = t_c.id_teacher
JOIN Book b
ON t_c.id_book = b.id;

CREATE VIEW StudentsWhoDidNotReturnBooks AS
SELECT s.last_name, s_c.date_in
FROM Student s JOIN S_Cards s_c
ON s.id = s_c.id_student
WHERE s_c.date_in IS NULL;

CREATE VIEW StudentsWhoNeverBorrowedBooks AS
SELECT s.last_name
FROM Student s
WHERE s.id NOT IN (SELECT s_c.id_student FROM S_Cards s_c WHERE s_c.id_student IS NOT NULL)

CREATE VIEW MostActiveLibrarian AS
SELECT TOP 1 last_name, SUM(amount) AS total_count
FROM 
	(SELECT l.last_name, COUNT(t_c.id_librarian) AS amount
	FROM Librarian l JOIN T_Cards t_c
	ON l.id = t_c.id_librarian
	GROUP BY l.last_name

	UNION ALL

	SELECT l.last_name, COUNT(s_c.id_librarian)
	FROM Librarian l JOIN S_Cards s_c
	ON l.id = s_c.id_librarian
	GROUP BY l.last_name) AS temp_result
GROUP BY last_name
ORDER BY 2 DESC

CREATE VIEW MostResponsibleLibrarian AS
SELECT TOP 1 last_name, SUM(amount) AS total_count
FROM 
	(SELECT l.last_name, COUNT(t_c.id_librarian) AS amount
	FROM Librarian l JOIN T_Cards t_c
	ON l.id = t_c.id_librarian
	WHERE t_c.date_in IS NOT NULL
	GROUP BY l.last_name

	UNION ALL

	SELECT l.last_name, COUNT(s_c.id_librarian)
	FROM Librarian l JOIN S_Cards s_c
	ON l.id = s_c.id_librarian
	WHERE s_c.date_in IS NOT NULL
	GROUP BY l.last_name) AS temp_result
GROUP BY last_name
ORDER BY 2 DESC
