# BigData

#build.sbt
import sbtassembly.MergeStrategy
ThisBuild / version := "0.1.0-SNAPSHOT"
ThisBuild / scalaVersion := "2.13.15"
lazy val root = (project in file("."))
  .settings(
    name := "scalaSpark"
  )
ThisBuild / assemblyMergeStrategy := {
  case "META-INF/services/org.apache.spark.sql.sources.DataSourceRegister" => MergeStrategy.concat
  case PathList("META-INF", xs @ _*) => MergeStrategy.discard
  case x => MergeStrategy.first
}
val sparkVersion = "3.4.3"
val hadoopVersion = "3.2.4"

libraryDependencies ++= Seq(

  "org.apache.spark" %% "spark-core" % sparkVersion % "provided",
  "org.apache.spark" %% "spark-sql" % sparkVersion % "provided",
  "org.apache.spark" %% "spark-hive" % sparkVersion,
  "org.apache.hadoop" % "hadoop-hdfs-native-client" % "3.2.4",
  "mysql" % "mysql-connector-java" % "8.0.33",
  "io.delta" %% "delta-core" % "2.4.0",
  "org.postgresql" % "postgresql" % "42.7.3"
)

resolvers ++= Seq("Delta Lake Repository" at "https://packages.delta.io/maven",

  "Confluent" at "https://packages.confluent.io/maven/")

