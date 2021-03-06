

.. _logging:

====
ログ出力
====

PHPUnit は、いくつかの形式のログファイルを作成することができます。

.. _logging.xml:

テスト結果 (XML)
###########

PHPUnit が作成するテスト結果の XML のログファイルは、
`Apache Ant の JUnit タスク <http://ant.apache.org/manual/Tasks/junit.html>`_
が使用しているものを参考にしています。
以下の例は、``ArrayTest`` のテストが生成した
XML ログファイルです。

.. code-block:: bash

    <?xml version="1.0" encoding="UTF-8"?>
    <testsuites>
      <testsuite name="ArrayTest"
                 file="/home/sb/ArrayTest.php"
                 tests="2"
                 assertions="2"
                 failures="0"
                 errors="0"
                 time="0.016030">
        <testcase name="testNewArrayIsEmpty"
                  class="ArrayTest"
                  file="/home/sb/ArrayTest.php"
                  line="6"
                  assertions="1"
                  time="0.008044"/>
        <testcase name="testArrayContainsAnElement"
                  class="ArrayTest"
                  file="/home/sb/ArrayTest.php"
                  line="15"
                  assertions="1"
                  time="0.007986"/>
      </testsuite>
    </testsuites>

次の XML ログファイルは、テストクラス
``FailureErrorTest`` にある 2 つのテスト
``testFailure`` および ``testError``
が出力したものです。失敗やエラーがどのように表示されるのかを確認しましょう。

.. code-block:: bash

    <?xml version="1.0" encoding="UTF-8"?>
    <testsuites>
      <testsuite name="FailureErrorTest"
                 file="/home/sb/FailureErrorTest.php"
                 tests="2"
                 assertions="1"
                 failures="1"
                 errors="1"
                 time="0.019744">
        <testcase name="testFailure"
                  class="FailureErrorTest"
                  file="/home/sb/FailureErrorTest.php"
                  line="6"
                  assertions="1"
                  time="0.011456">
          <failure type="PHPUnit_Framework_ExpectationFailedException">
    testFailure(FailureErrorTest)
    Failed asserting that &lt;integer:2&gt; matches expected value &lt;integer:1&gt;.

    /home/sb/FailureErrorTest.php:8
    </failure>
        </testcase>
        <testcase name="testError"
                  class="FailureErrorTest"
                  file="/home/sb/FailureErrorTest.php"
                  line="11"
                  assertions="0"
                  time="0.008288">
          <error type="Exception">testError(FailureErrorTest)
    Exception:

    /home/sb/FailureErrorTest.php:13
    </error>
        </testcase>
      </testsuite>
    </testsuites>

.. _logging.codecoverage.xml:

コードカバレッジ (XML)
##############

PHPUnit がコードカバレッジ情報のログ出力の際に使用している XML のフォーマットは、
`Clover <http://www.atlassian.com/software/clover/>`_
のものを参考にしています。
以下の例は、``BankAccountTest`` のテストが生成した
XML ログファイルです。

.. code-block:: bash

    <?xml version="1.0" encoding="UTF-8"?>
    <coverage generated="1184835473" phpunit="4.8.0">
      <project name="BankAccountTest" timestamp="1184835473">
        <file name="/home/sb/BankAccount.php">
          <class name="BankAccountException">
            <metrics methods="0" coveredmethods="0" statements="0"
                     coveredstatements="0" elements="0" coveredelements="0"/>
          </class>
          <class name="BankAccount">
            <metrics methods="4" coveredmethods="4" statements="13"
                     coveredstatements="5" elements="17" coveredelements="9"/>
          </class>
          <line num="77" type="method" count="3"/>
          <line num="79" type="stmt" count="3"/>
          <line num="89" type="method" count="2"/>
          <line num="91" type="stmt" count="2"/>
          <line num="92" type="stmt" count="0"/>
          <line num="93" type="stmt" count="0"/>
          <line num="94" type="stmt" count="2"/>
          <line num="96" type="stmt" count="0"/>
          <line num="105" type="method" count="1"/>
          <line num="107" type="stmt" count="1"/>
          <line num="109" type="stmt" count="0"/>
          <line num="119" type="method" count="1"/>
          <line num="121" type="stmt" count="1"/>
          <line num="123" type="stmt" count="0"/>
          <metrics loc="126" ncloc="37" classes="2" methods="4" coveredmethods="4"
                   statements="13" coveredstatements="5" elements="17"
                   coveredelements="9"/>
        </file>
        <metrics files="1" loc="126" ncloc="37" classes="2" methods="4"
                 coveredmethods="4" statements="13" coveredstatements="5"
                 elements="17" coveredelements="9"/>
      </project>
    </coverage>

.. _logging.codecoverage.text:

コードカバレッジ (テキスト)
###############

人間が読める形式のコードカバレッジ情報を、コマンドラインあるいはテキストファイルに出力します。

この出力フォーマットの狙いは、ちょっとしたクラス群のカバレッジの概要を手軽に把握することです。
大規模なプロジェクトでは、このフォーマットを使えばプロジェクト全体のカバレッジを大まかに把握しやすくなるでしょう。
``--filter`` と組み合わせて使うこともできます。
コマンドラインから使う場合は ``php://stdout`` に書き込みます。
この出力は ``--colors`` の設定を反映したものになります。
コマンドラインから使った場合は、デフォルトの出力先は標準出力となります。
デフォルトでは、テストで少なくとも一行はカバーしているファイルしか表示しません。
この設定は、xml の ``showUncoveredFiles`` オプションでしか変更できません。
:ref:`appendixes.configuration.logging` を参照ください。
デフォルトでは、すべてのファイルとそのカバレッジ情報が、詳細形式で表示されます。
この設定は、xml のオプション ``showOnlySummary`` で変更できます。


