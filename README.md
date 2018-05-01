# to do bootstrap arabic

<h4> حتى يعمل معك الموقع بدون مشاكل اعمل الخطوات التاليه </h4>

<b> إنشاء قاعدة بيانات بإسم  </b>
<pre> to_do </pre>
<b> بعدها انشاء الجداول التاليه</b>
<pre>

--
-- Table structure for table `subtasks`
--

DROP TABLE IF EXISTS `subtasks`;
CREATE TABLE IF NOT EXISTS `subtasks` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `task_id` int(11) NOT NULL,
  `description` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `due_date` date NOT NULL,
  `user_id` int(11) NOT NULL,
  `done` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `FK_t2_1` (`task_id`)
) ENGINE=MyISAM AUTO_INCREMENT=60 DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

-- --------------------------------------------------------
</pre>

<b>بعدها لاتنسى عمل  العملية التاليه حتى يتم حذف المهام الفرعية عند حذف المهمة الرئيسية </b>
<br>
<b> create trigger </b>
<pre>

--
-- Triggers `tasks`
--
DROP TRIGGER IF EXISTS `deleteSutask`;
DELIMITER $$
CREATE TRIGGER `deleteSutask` BEFORE DELETE ON `tasks` FOR EACH ROW BEGIN
  DELETE FROM subtasks WHERE subtasks.task_id = OLD.id;
END
$$
DELIMITER ;
COMMIT;

</pre>

<b> تغير الاعداد التاليه على حسب السيرفر المحلي إلي في جهازك </b>
<br>
<b> app/config.php </b>
<pre>

// Set configurations
$server_name = 'localhost';
$user_name = 'root';
$password = '';
$dbname = 'to_do';

</pre>

<b>  اخر خطوة وضع المجلد كامل في مسار السيرفر المحلي مثال  </b>
<br>
<b> wampserver path C:\wamp64\www\ </b>


