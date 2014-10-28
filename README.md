inflater = (LayoutInflater) getSystemService(Context.LAYOUT_INFLATER_SERVICE);
alarmManager = (AlarmManager) getSystemService(Context.ALARM_SERVICE);
@Override
public void onClick(View v)
{
	
	
		setAlarm = (LinearLayout) inflater.inflate(
				R.layout.alarm_dialog, null);
		timePicker = (TimePicker) setAlarm
				.findViewById(R.id.timepicker);
		new AlertDialog.Builder(MainActivity.this)
				.setView(setAlarm)
				.setTitle("��������ʱ��")
				.setPositiveButton("ȷ��",
						new DialogInterface.OnClickListener()
						{
							@Override
							public void onClick(DialogInterface dialog,
									int which)
							{
								alarmManager.cancel(pi);
								c.set(Calendar.HOUR_OF_DAY,
										timePicker.getCurrentHour());        // ��������Сʱ��
								c.set(Calendar.MINUTE,
										timePicker.getCurrentMinute());            // �������ӵķ�����
								c.set(Calendar.SECOND, 0); // �������ӵ�����
								c.set(Calendar.MILLISECOND, 0); // �������ӵĺ�����

								btn.setText(sdf.format(new Date(c
										.getTimeInMillis())));
								intent = new Intent(MainActivity.this,
										AlarmReceiver.class);    // ����Intent����
								pi = PendingIntent
										.getBroadcast(
												MainActivity.this, 0,
												intent, 0);    // ����PendingIntent

								alarmManager.setRepeating(
										AlarmManager.RTC,    // �������ӣ���ǰʱ��ͻ���
										c.getTimeInMillis(),
										24 * 60 * 60 * 1000, pi);

								Toast.makeText(MainActivity.this,
										"�������óɹ�", Toast.LENGTH_LONG)
										.show();// ��ʾ�û�
							}
						}).setNegativeButton("ȡ��", null).show();
	
	
}