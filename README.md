# Guanlixinxixitong
## Sql语句：
CREATE TABLE `person` (
  `保养人id` int(11) NOT NULL auto_increment,
  `保养人名称` varchar(45) NOT NULL,
  PRIMARY KEY  (`保养人id`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;<br>
CREATE TABLE `cost` (
  `消耗id` int(11) NOT NULL auto_increment,
  `记录id` int(11) NOT NULL,
  `消耗材料` varchar(45) NOT NULL,
  `消耗数量` int(11) NOT NULL,
  `单位` varchar(45) NOT NULL,
  PRIMARY KEY  (`消耗id`),
  KEY `记录_idx` (`记录id`),
  CONSTRAINT `记录` FOREIGN KEY (`记录id`) REFERENCES `保养记录` (`记录id`) ON DELETE NO ACTION ON UPDATE NO ACTION
) ENGINE=InnoDB DEFAULT CHARSET=latin1;<br>
CREATE TABLE `保养记录` (
  `记录id` int(11) NOT NULL auto_increment,
  `设备id` int(11) NOT NULL,
  `项目id` int(11) NOT NULL,
  `保养人id` int(11) NOT NULL,
  `时间` date NOT NULL,
  `备注` text,
  PRIMARY KEY  (`记录id`),
  KEY `设备_idx` (`设备id`),
  KEY `项目_idx` (`项目id`),
  KEY `保养人id_idx` (`保养人id`),
  CONSTRAINT `设备` FOREIGN KEY (`设备id`) REFERENCES `设备` (`设备id`) ON DELETE NO ACTION ON UPDATE NO ACTION
) ENGINE=InnoDB DEFAULT CHARSET=latin1;<br>
CREATE TABLE `保养项目` (
  `项目id` int(11) NOT NULL auto_increment,
  `项目内容` varchar(45) NOT NULL,
  PRIMARY KEY  (`项目id`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;<br>
CREATE TABLE `设备` (
  `设备id` int(11) NOT NULL auto_increment,
  `设备名称` varchar(45) NOT NULL,
  `设备类型id` int(11) NOT NULL,
  `最后保养时间` varchar(45) NOT NULL,
  PRIMARY KEY  (`设备id`),
  KEY `设备类型_idx` (`设备类型id`),
  CONSTRAINT `设备类型` FOREIGN KEY (`设备类型id`) REFERENCES `设备类型` (`类型id`) ON DELETE NO ACTION ON UPDATE NO ACTION
) ENGINE=InnoDB DEFAULT CHARSET=latin1;<br>
CREATE TABLE `设备类型` (
  `类型id` int(11) NOT NULL auto_increment,
  `类别名称` varchar(45) NOT NULL,
  `项目id` int(11) NOT NULL,
  `保养周期` varchar(45) NOT NULL,
  PRIMARY KEY  (`类型id`),
  KEY `项目_idx` (`项目id`),
  CONSTRAINT `项目` FOREIGN KEY (`项目id`) REFERENCES `保养项目` (`项目id`) ON DELETE NO ACTION ON UPDATE NO ACTION
) ENGINE=InnoDB DEFAULT CHARSET=latin1;<br>
SELECT 设备.设备id,设备.设备id,设备.最后保养时间
 FROM 保养记录 AS a,设备 AS b,设备类型 AS c 
 WHERE a.设备号=b.设备号 
 and b.设备类型=c.设备类型名 
 and curdate()-b.保养时间<30
SELECT b.设备id,b.设备类型id,b.最后保养时间
 FROM 保养记录 AS a,设备 AS b,设备类型 AS c 
 WHERE a.设备id=b.设备id
 and b.设备类型id=c.类型名id
 and curdate()-b.最后保养时间<30
  
  Axure原型（项目名：维修保养 密码：123456）: 
 http://vyjv9j.axshare.com <br>
  ER图: http://pan.baidu.com/s/1kVJKIzl
 
