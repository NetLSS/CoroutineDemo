# 코틀린 코투린 예제 프로젝트

- SeekBar progress 만큼 코루틴 실행 (최대 2000)

[라이브러리 종속성 추가]
```groovy
    implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-core:1.4.1'
    implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-android:1.4.1'
```

[코루틴 코드 예시]
```kotlin
    private val coroutineScope = CoroutineScope(Dispatchers.Main)

    suspend fun performTask(taskNumber: Int): Deferred<String> =
        coroutineScope.async(Dispatchers.Main) {
            delay(7_777)
            return@async "Finished Coroutine $taskNumber"
        }

    fun launchCoroutines(view: View) {
        (1..count).forEach {
            binding.statusText.text = "Started Coroutine $it"
            coroutineScope.launch(Dispatchers.Main) {
                binding.statusText.text = performTask(it).await()
            }
        }
    }
```